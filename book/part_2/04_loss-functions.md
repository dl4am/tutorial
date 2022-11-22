# Loss Functions

As discussed throughout Section 2.4, the loss function is a critical component of the learning system. While there are many considerations regarding loss functions for applications in audio signal processing, we will discuss in this section the most important aspects that are relevant for constructing an automatic mixing system. Most audio-focused loss functions can be categorised in

## Time domain

## Frequency domain

## Stereophonic

An important consideration for multitrack mixing systems is how our loss function considers stereophonic information. Unlike many other applications in audio signal processing, such as speech, proper stereo balance is a critical part of the mixing process

In the following sections we will demonstrate how to generate mixes with pretrained models as well as understand their implementation, and how to train them.

{cite}`steinmetz2020auraloss`

## Deep Feature