# Metadata

In addition to the core metadata recommendations listed in the [Extensibility documentation](IR.md) there is additional experimental metadata to help provide information for inputs and outputs to the model.  

This metadata applies to all inputs and outputs tensors of a given category.    The first such category we define is : `Image`.

## Motivation

The motivation of such a mechanism is to allow model authors to convey to model consumers enough information for them to use the model.    If an image is being passed into this model, it is important to know enough
about the image so that proper featurization can happen prior to using the model.   

Note: full featurization support is a NON GOAL of this proposal. The goal is simply to provide enough metadata that the model consumer can perform their own featurization in and out of the model.

## Image Category Definition

For every tensor in this model that uses [Tensor Denotation](TensorDenotation.md) to declare itself an image, you can provide more information about those images that are global to the entire model.

Specifically, in our first proposal, we define the following set image metadata:

|Key|Value|Description|
|-----|----|-----------|
|`Image.BitmapPixelFormat`|__string__| Specifies the pixel format of pixel data. Each enumeration value defines a channel ordering and bit depth. Possible values : <ul><li>Gray8</li><ul><li>1 channel image, the pixel data is 8 bpp grayscale.</li></ul><li>Rbg8</li><ul><li>3 channel image, channel order is RBG, pixel data is 8bpp.  no alpha</li></ul><li>Bgr8</li><ul><li>3 channel image, channel order is BGR, pixel data is 8bpp.  no alpha</li></ul><li>Rgba8</li><ul><li>4 channel image, channel order is RGBA, pixel data is 8bpp.  Straight alpha</li></ul><li>Bgra8</li><ul><li>4 channel image, channel order is BGRA, pixel data is 8bpp.  Straight alpha</li></ul></ul>|
|`Image.ColorSpaceGamma`|__string__| describes that a tensor holds an audio clip.|
|`Image.NormalizedPixelRange`|__string__| describes that a tensor holds a block of text.|


		
