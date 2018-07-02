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

The __Session constructor__ controls 3 things:
- _The var_list_ to be used in case of a distributed architecture to handle computation. You can specify which TF server or ‘target’ you want to compute on.
- Which __graph__ the Session will handle. The tricky things for beginners, is the fact that there is always a default Graph in TF where all operations are set by default, so you are always in a “default Graph scope”.
- The config: You can use `ConfigProto` to configure TF.
