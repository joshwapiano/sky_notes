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

Different methods for training model e.g. Amazon Web Services https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-classification-aws.md
Another AWS method, using 'Sagemaker' machine for GPU - https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-classification-mxnet-sagemaker.md which uses Amazon's preferred 'MXnet' https://en.wikipedia.org/wiki/Apache_MXNet
Their final example method which uses local GPU! But this is for the second stage of the project https://github.com/joshwapiano/label-maker/blob/master/examples/walkthrough-tensorflow-object-detection.md

#### How advanced would the land use classification need to be? Probably only one Neural Net could achieve accuracy required here.

