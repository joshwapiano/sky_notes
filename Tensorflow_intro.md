# Tensorflow basics from Morgan at Metaflow

### 'Tensorflow: A primer'
###### https://blog.metaflow.fr/tensorflow-a-primer-4b3fa0978be3

TF blurs the line between mathematical operations and the actual results
When you write math in TF, you have to think about it as an architect. You are designing operations and not calculating things.

Everything that “happens” in TF, “happens” within a __Session__.

So when you “add” something in TF, you are designing an “add” operation, not actually adding anything. All those operations are organised as a __Graph__, your __Graph__ holds _operations_ and _tensors_, not values.

When you start what is called a __Session__, you actually create a new scope for your program where operations can “happen”. This is where you can run/evaluate operations and tensors. And when you do so, results start to unravel: tensors get filled with real values, operations get computed, results are obtained, functions converge, etc.

But as soon as you get out of the scope of your __Session__, the __Graph__ returns to its static and quite boring state.

To summarise - there are two main phases in TF code:
1.  The __Graph level__: You can design mathematical and control flow operations which will be the different parts of your __Graph__. At this level, you can only save your __Graph__ itself and its __metadata__, nothing tangible exists yet.
2.  The __Session and evaluation level__: variables get initialised, other book keeping functions gets configured, operations get executed, intermediary tensors and gradients get calculated, etc.

__The most important part is that only variables keeps their data between multiple session evaluations.__
_All other tensors are temporary which means that they will be destroyed and inaccessible in your training for-loop without a proper feed_dict or any other input pipeline of your choice._ __This is very memory efficient__

### [Shapes in TF](https://blog.metaflow.fr/shapes-and-dynamic-dimensions-in-tensorflow-7b1fe79be363)

__Tensors in TensorFlow have 2 shapes: The static shape AND the dynamic shape!__
__The static shape__ is the shape you provided when creating a tensor OR the shape inferred by TensorFlow when you define an operation resulting in a new tensor. It is a tuple or a list.
```
my_tensor = tf.constant(47., shape=[2,3,2])
print(my_tensor) # -> Tensor("Const:0", shape=(2, 3, 2), dtype=float32)
```
__The dynamic shape__ is the actual one used when you run your graph. It is itself a tensor describing the shape of the original tensor.

```
print(my_tensor.eval(session=tf.Session()))
[[[47. 47.]
  [47. 47.]
  [47. 47.]]

 [[47. 47.]
  [47. 47.]
  [47. 47.]]]
```

Use the static shape for debugging
Use the dynamic shape everywhere else especially when you have undefined dimensions

### 'TensorFlow: saving/restoring and mixing multiple models'
###### https://blog.metaflow.fr/tensorflow-saving-restoring-and-mixing-multiple-models-c4c94d5d7125

#### How to actually save and load something
##### The Saver and Session object
Any interaction with your filesystem to save persistent data in TF needs a [Saver object](https://www.tensorflow.org/api_docs/python/tf/train/Saver) and a [Session object](https://www.tensorflow.org/api_docs/python/tf/Session).

The __Saver constructor__ allows control of the _var_list_: (Default `None`), this is the list of variables that will persist within the filesystem. You can either choose to save all the variables, some variables or even a dictionary to give custom names to your variables.
The Saver handles the saving and loading (called restoring) of your Graph metadata and your Variables data. To do that, it adds operations inside the current Graph that will be evaluated within a session.
By default, the Saver will handle the default Graph and all its included Variables, but you can create as much Savers as you want to control any graph or subgraph and their variables.

The __Session constructor__ controls 3 things:
- _The var_list_ to be used in case of a distributed architecture to handle computation. You can specify which TF server or ‘target’ you want to compute on.
- Which __graph__ the Session will handle. The tricky things for beginners, is the fact that there is always a default Graph in TF where all operations are set by default, so you are always in a “default Graph scope”.
- The config: You can use `ConfigProto` to configure TF.

```
import tensorflow as tf

import os
dir = os.path.dirname(os.path.realpath(__file__))

# Currently, we are in the default graph scope

# Let's design some variables
v1 = tf.Variable(1. , name="v1")
v2 = tf.Variable(2. , name="v2")
# Let's design an operation
a = tf.add(v1, v2)

# We can check easily that we are indeed in the default graph
print(a.graph == tf.get_default_graph())
# -> True

# Let's create a Saver object
# By default, the Saver handles every Variables related to the default graph
all_saver = tf.train.Saver() 
# But you can precise which vars you want to save (as a list) and under which name (with a dict)
v2_saver = tf.train.Saver({"v2": v2}) 


# By default the Session handles the default graph and all its included variables
with tf.Session() as sess:
  # Init v1 and v2   
  sess.run(tf.global_variables_initializer())
  # Now v1 holds the value 1.0 and v2 holds the value 2.0
  # and we can save them
  all_saver.save(sess, dir + '/data-all')
  # or saves only v2
  v2_saver.save(sess, dir + '/data-v2')
  ```
  
  [Protocol Buffers, often abreviated __Protobufs__, is the format used by TF to store and transfer data efficiently.](https://developers.google.com/protocol-buffers/) Like a faster XML or JSON format that can be compressed after development from .pbtxt to .pb to save space/bandwidth for storage/transfer in production.
  

The (.meta, .index, .data) trio of checkpoint files store the compressed data about your models and its weights.
- The __checkpoint file__ is just a bookkeeping file that you can use in combination of high-level helper for loading different time saved chkp files.
- The __.meta file__ holds the compressed Protobufs graph of your model and all the metadata associated (collections, learning rate, operations, etc.)
- The __.index file__ holds an immutable key-value table linking a serialised tensor name and where to find its data in the chkp.data files
- The __.data files__ hold the data (weights) itself (this one is usually quite big in size). There can be many data files because they can be sharded and/or created on multiple timesteps while training.
- Finally, the __events file__ store everything you need to visualise your model and all the data measured while you were training using summaries. This has nothing to do with saving/restoring your models itself.
