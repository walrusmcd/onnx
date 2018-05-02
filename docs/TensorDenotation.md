# Tensor Denotation

Tensor Denotation is an experimental attempt along with dimension denotation to give tensor semantic descriptions and enable model authors to describe what the input and output tensors are.

## Motivation

The motivation of such a mechanism can be illustrated via a simple example. In the the neural network SqueezeNet, it takes in a NCHW image input float[1,2,244,244] and produces a output of float[1,1000,1,1]:

```
input_in_NCHW -> SqueezeNet() -> output_softmaxout_1
```

In this case the user needs to know that the input is an image, that the image is in the format of NCHW, and that the color channels in there are bgr.

This proposal consists of three key components: Tensor Denotation, [Dimension Denotation](DimensionDenotation.md), and model metadata_props.  Each of which will be discussed in detail.

## Tensor Denotatio Definition

To begin with, we define a set of semantic types that models consume as inputs and produce as outputs.

Specifically, in our first proposal, we define the following set of standard denotations:

1. `IMAGE` describes that a tensor holds an image.  You can use dimension denotation to learn more about the layout of the image, and also the optional model metadata_props.
2. `AUDIO` describes that a tensor holds an audio clip.   
3. `TEXT` describes that a tensor holds a block of text.

Model authors SHOULD add tensor denotation to inputs and outputs for the type of tensors they expect for the model.

## Denotation Propagation

For tensors, Denotation Propagation does not automatically occur.   It is used to describe the initial input or final outputs, but as data flows through the graph no inference is made to propogate if the data still holds an image (for example).   A model builder or conversion tool MAY apply propagation manually in the model if it knows that subsequent tensors share the same semantic denotation.

## Denotation Verification

Denotation Verification is not enforced.   It is simply a method for model authors to indicate to model consumers what they should be passing in and what they should be expecting out.  No error is reported if you do not actually pass in an image (for example).

## Dimension Denotation

Tensor denotation can be combined with the new experimental feature of Dimension Denotation.  For example if the Tensor Denotation is `IMAGE`, then that tensor SHOULD also have Dimension Denotation stating the NCHW channel layout.  (described as [`DATA_BATCH`, `DATA_CHANNEL`, `DATA_FEATURE`, `DATA_FEATURE`]).

## Model metadata_props

Optional metadata can be provided on the model to describe information about ALL inputs and outputs for the model.   For example, image.BitmapPixelFormat.  See the [model metadata_props documentation](MetadataProps.md) for details.