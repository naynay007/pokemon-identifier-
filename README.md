# pokemon-identifier-

 
 # this AI will identify an image/video of a pokemon wether it is bulbasaur, squirtle or charmander.


![image](https://github.com/naynay007/pokemon-identifier-/assets/108524891/addcc76c-6d6e-4e34-8ee0-8f1fa6480a43)


## The Algorithm
to classify an image, AI uses a thing called "Image classification". Image classification is a supervised learning problem: define a set of target classes (objects to identify in images), and train a model to recognize them using labeled example photos. Raw pixel data alone doesn't provide a sufficiently stable representation to encompass the myriad variations of an object as captured in an image. The position of the object, background behind the object, ambient lighting, camera angle, and camera focus all can produce fluctuation in raw pixel data.

The pokemon can be captured in a photo in a variety of poses, with different backdrops and lighting conditions. Averaging pixel data to account for this variety does not produce any meaningful information. An example of what this looks like to the computer, but with a database of cats is this:
![image](https://github.com/naynay007/pokemon-identifier-/assets/108524891/7c431636-eca1-4f8a-8663-fee0b0ed4c25)
to solve this issue, a method is used called "Convolutional neural networks", or "CNN".

> Convolutional neural networks (CNN)
A breakthrough in building models for image classification came with the discovery that a convolutional neural network (CNN) could be used to progressively extract higher- and higher-level representations of the image content. Instead of preprocessing the data to derive features like textures and shapes, a CNN takes just the image's raw pixel data as input and "learns" how to extract these features, and ultimately infer what object they constitute.

>To start, the CNN receives an input feature map: a three-dimensional matrix where the size of the first two dimensions corresponds to the length and width of the images in pixels. The size of the third dimension is 3 (corresponding to the 3 channels of a color image: red, green, and blue). The CNN comprises a stack of modules, each of which performs three operations.
>https://developers.google.com/machine-learning/practica/image-classification/convolutional-neural-networks#1_convolution
## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.

[View a video explanation here](video link)
