# Tensorflow basics from Morgan at Metaflow

### 'Tensorflow: A primer'
###### https://blog.metaflow.fr/tensorflow-a-primer-4b3fa0978be3

TF blurs the line between mathematical operations and the actual results
When you write math in TF, you have to think about it as an architect. You are designing operations and not calculating things.
Everything that “happens” in TF, “happens” within a __Session__.

So when you “add” something in TF, you are designing an “add” operation, not actually adding anything. All those operations are organised as a __Graph__, your __Graph__ holds _operations_ and _tensors_, not values.
