# Mix-Wave-U-Net

The Mix-Wave-U-Net {cite}`martinez2021deep` is based upon the Wave-U-Net architecture {cite}`stoller2018wave`, a model proposed for music source separation. This approach leverages the fact that the generation of a multitrack mix in many ways is the inverse task of separating the sources in a mixture, the focus of music source separation systems. In this work, the authors demonstrated how to train a Wave-U-Net model to map individual recordings to the final mixture by adjusting the number of inputs to the system to accept the multitrack input, and adjusting the number of outputs to two, which produces a stereo mix.

```{figure} /assets/figures/mix-wave-u-net.svg
:name: mix-wave-u-net
:alt: Mix-Wave-U-Net
:align: center

Mix-Wave-U-Net architecture based upon the Wave-U-Net, which is composed of a series of downsampling and upsampling blocks with skip connections.
```

The Wave-U-Net model itself is actually based on a seminal model proposed for computer vision tasks known as the U-Net, which was proposed for image segmentation {cite}`ronneberger2015u`. Unlike other source separation models that operate on magnitude or complex spectrograms, Wave-U-Net operates on mixture directly in the time domain, using 1-d convolutions to progressively process the signal. It can be viewed as an encoder-decoder or autoencoder network. 

In the encoder the signal is progressively downsampled until a certain resolution is reached, which is a function of the number of downsampling operations. This is achieved by stacking a number of downsampling blocks in series. Each downsampling block follows a similar structure. It includes a 1-d convolution followed by a nonlinear activation (in the original implementation this is  LeakyReLU). After these operations a downsampling or decimation operation is performed which decreases the temporal resolution of the intermediate activations by a factor of two. In the original paper the authors implement this with a straightforward decimation, but it can also be implemented with a strided convolution.

At each downsampling block, the temporal resolution is repeatedly decreased. This results in a shorter and shorter signal in the time domain, while the number of convolutional channels is increased by $F_c=24$ at each block. At the final downsampling block another 1-d convolution is applied, before the signal is passed on to a series of upsampling blocks which in some sense mirror the downsampling blocks. 

The downsampled representation is sent through a decoding process and the intermediate activations are progressively upsampled. Unique to the U-Net-like architectures is the inclusion of skip connections (denoted as dashed arrows) that shuttle information from each layer of the encoder to their respective layer in the decoder. This enables combining information from the downsampled signal at various temporal resolutions to the upsampling process during signal reconstruction. Empirically this has been shown to lead to improved performance and accuracy in the reconstruction quality. 

It should be noted that Wave-U-Net also has close connection to other encoder-decoder architectures for audio signal processing, most noticeable of which is Demucs and its variants {cite}`defossez2019music`. Demucs builds on the Wave-U-Net with some architectural adjustments, namely the use of more aggressive downsampling operations, the use a recurrent neural network in the embedding layer, as well as transposed convolutions for upsampling. These modifications were shown to lead to improved source separation performance following a similar U-Net inspired architecture.

As a direct transformation method, Mix-Wave-U-Net was shown to produce impressive results in that it was able to mimic the mixes in the ENST-drums dataset. This meant the system was capable of mimicking the equalization, compression, and reverberation of the target mixes without any explicit knowledge of these effects. However, this model has the ability to impart undesirable artifacts when out-of-distribution input recordings are used. 
In addition, since this is a direct transformation method users are not aware of the mixing process and have no control over the final result. 