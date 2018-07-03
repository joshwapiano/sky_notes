# Working notes on land use classification

Recap of difficulties/importance attaining labelled data

## Google Earth Engine

First benefits or GEE, why this could be great tool
Then discussion on attempt to use Python API, issues faced, why javascript API decided upon
Then discussion on lack of Landsat 8 data for ROI from investigation - see notes with Tom Jones
Then attempts using Sentinel 2.. TBC


## Mapbox, OSM (Open Street Map) QA Data tiles, 

What OSM is, what Mapbox is.
Method for acquiring labelled data in .npz format, discuss which countries could form best training data for South China Sea etc. Could use https://github.com/mapbox/mbview to view data to visually inspect.

Lots of different Keras Models:
https://keras.io/applications/#documentation-for-individual-models

Different methods for training model e.g. Amazon Web Services https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-classification-aws.md and ResNet50 (Keras)
Another AWS method, using 'Sagemaker' machine for GPU - https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-classification-mxnet-sagemaker.md which uses Amazon's preferred non-keras/tensorflow: 'MXnet' https://www.allthingsdistributed.com/2016/11/mxnet-default-framework-deep-learning-aws.html
https://en.wikipedia.org/wiki/Apache_MXNet
AWS also supports Caffe, CNTK, TensorFlow, Theano, and Torch.

AWS Student Account is jsteph06@mail.bbk.ac.uk  Fre...13
Mapbox pk.eyJ1Ijoiam9zaHdhcGlhbm8iLCJhIjoiY2ppaXVqb2pkMXBrazNxa2h5Z2ppeXVnNyJ9.D4GlGxOe7O3BUolcrmoqSg
Planet Labs user is jsteph06@mail.bbk.ac.uk  Fre...13
GBDX user is jsteph06@mail.bbk.ac.uk Fre...13

Development Seed's label-maker final example method actually uses local GPU! But this is for the second stage of the project https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-tensorflow-object-detection.md

#### How advanced would the land use classification need to be? Probably only one Neural Net could achieve accuracy required here.

Phil Stubbins ONS used SegNet for his Skywalker project, also mentions UNet, Deeplab Resnet, DilatedNet in Keras

For Part II higher-res object detection combine multiple and use [ridge regression model](https://en.wikipedia.org/wiki/Tikhonov_regularization)?

VGG-16, ResNet
Understanding Amazon from space - Kaggle, used 11 CNNs - This is pretty nice, details winners' end-to-end architecture. simplenet, inception v3, resnet_34 *_50 *_101 *_152, resnet dilation, densenet121 161 169 201
http://blog.kaggle.com/2017/10/17/planet-understanding-the-amazon-from-space-1st-place-winners-interview/
FMoW https://github.com/fMoW - First place used 12 Deep-Path 92 Networks https://github.com/cypw/DPNs, 2nd place used three MXnet models, 3rd place used the 'Hydra' framework which is an ensemble of ResNet and DenseNet architectures https://arxiv.org/abs/1802.03518
