# pokemon-identifier-

 
 # this AI will identify an image/video of a pokemon wether it is bulbasaur, squirtle or charmander.


![image](https://github.com/naynay007/pokemon-identifier-/assets/108524891/addcc76c-6d6e-4e34-8ee0-8f1fa6480a43)


## The Algorithm
to classify an image, AI uses a thing called "Image classification". Image classification is a supervised learning problem: define a set of target classes (objects to identify in images), and train a model to recognize them using labeled example photos. Raw pixel data alone doesn't provide a sufficiently stable representation to encompass the myriad variations of an object as captured in an image. The position of the object, background behind the object, ambient lighting, camera angle, and camera focus all can produce fluctuation in raw pixel data.

The pokemon can be captured in a photo in a variety of poses, with different backdrops and lighting conditions. Averaging pixel data to account for this variety does not produce any meaningful information. An example of what this looks like to the computer, but with a database of cats is this:
![image](https://github.com/naynay007/pokemon-identifier-/assets/108524891/7c431636-eca1-4f8a-8663-fee0b0ed4c25)
    **to solve this issue, a method is used called "Convolutional neural networks", or "CNN".**

> Convolutional neural networks (CNN)
A breakthrough in building models for image classification came with the discovery that a convolutional neural network (CNN) could be used to progressively extract higher- and higher-level representations of the image content. Instead of preprocessing the data to derive features like textures and shapes, a CNN takes just the image's raw pixel data as input and "learns" how to extract these features, and ultimately infer what object they constitute.

>To start, the CNN receives an input feature map: a three-dimensional matrix where the size of the first two dimensions corresponds to the length and width of the images in pixels. The size of the third dimension is 3 (corresponding to the 3 channels of a color image: red, green, and blue). The CNN comprises a stack of modules, each of which performs three operations.
### Convolution
>A convolution extracts tiles of the input feature map, and applies filters to them to compute new features, producing an output feature map, or convolved feature (which may have a different size and depth than the input feature map). Convolutions are defined by two parameters:

> 1.**Size of the tiles that are extracted (typically 3x3 or 5x5 pixels).**
> 
> 2.**The depth of the output feature map, which corresponds to the number of filters that are applied.**

>During a convolution, the filters (matrices the same size as the tile size) effectively slide over the input feature map's grid horizontally and vertically, one pixel at a time, extracting >each corresponding tile (see Figure 1).

Fig 1:
![convolution_overview](https://github.com/naynay007/pokemon-identifier-/assets/108524891/09de1864-a9e8-4718-a65c-680e838bbb26)


>A 3x3 convolution over a 4x4 feature
map Figure 1. A 3x3 convolution of depth 1 performed over a 5x5 input feature map, also of depth 1. There are nine possible 3x3 locations to extract tiles from the 5x5 feature map, so this convolution produces a 3x3 output feature map.

>In Figure 1, the output feature map (3x3) is smaller than the input feature map (5x5). If you instead want the output feature map to have the same dimensions as the input feature map, you can add padding (blank rows/columns with all-zero values) to each side of the input feature map, producing a 7x7 matrix with 5x5 possible locations to extract a 3x3 tile.

>For each filter-tile pair, the CNN performs element-wise multiplication of the filter matrix and the tile matrix, and then sums all the elements of the resulting matrix to get a single value. Each of these resulting values for every filter-tile pair is then output in the convolved feature matrix which looks like this:
>
>![image](https://github.com/naynay007/pokemon-identifier-/assets/108524891/a95ca5d1-f7fa-44f5-812b-6b6172d1f6de)

>![Capture](https://github.com/naynay007/pokemon-identifier-/assets/108524891/465d433b-2646-49af-932a-bd0b587edfb7)
>
> **In short, CNN puts the image through a filter to simplify the information, allowing it to learn the optimal values for the filter matrices that enables it to extract meaningful features (textures, edges, shapes) from the input feature map.**

### how the AI is trained
The AI will look at a train file, containing data sets that it will learn off of and validate its training periodically after each enoch(cycle of training) in a file named "val". after a set amount of enochs have been completed, the client may test the program via the "test file" containing images the AI has never seen before. images can be easily imported into these files as well.
during the test, it will output what it thinks the image/video is depicting with a percentage of how sure the program is.



## Running this project

## How to set up the project
1. follow the instructions in this page https://student.idtech.com/courses/331/pages/old-re-training-image-classification-models-2?module_item_id=26828
2. open VS code
3. change directories to nvidia/jetson-inference/
4. run this command to overcommit memory:   echo 1 | sudo tee /proc/sys/vm/overcommit_memory
5. cd back to jetson-inference and enter: ./docker/run.sh
6. once in the docker container, change directories to  jetson-inference/python/training/classification
### now the terminal is all set for training, the data set just needs to be accesible.
7. create a file and order it in this order: (name of dataset, in this case:) pokemon > test, training and val.
   test, training and val files are stored within pokemon, te amount of data in each file shall be: 10% in test, 10% in val, and 80% in training.
   test, training and val will each contain the data that is being trained, in this case, bulbasaur, charmander and squirtle.
8.enter python3 train.py --model-dir=models/pokemon data/pokemon --enoch=100 to train the AI for 100 enochs. the enochs can be changed, although training should remain at a reasonable level to ensure overfitting does not occur (the AI finds for shortcuts to score high in the data given, but when handed new data will perform poorly)

## how to run this project 
1. exit the docker using crtl + D
2. enter: the jetson-inference/python/training/classification directory
3. enter: ls models/pokemon/
4. enter: NET=models/pokemon
5. enter: DATASET=data/pokemon
### the program is all set now, it is ready to be tested on an image/video
1. enter imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/Bulbasaur/03.png bulb2.png
   at the end: "$DATASET/test/Bulbasaur/03.png" is the image being tested, to change what image you want to test, import a file to the bulbasaur test directory, and change the 03.png with thr desired image/video. the bulb2.png at the end of the code is what the tested image will be known as, and will show the result of its decision:
![Capture](https://github.com/naynay007/pokemon-identifier-/assets/108524891/5b0278d3-f802-45f1-ae0e-5cfdf3ff31eb)


  


   




Granted the accuracy of this bublasaur is only 55.80%, it often scores higher in other images, and the accuracy of the AI can be improved via a larger dataset, and more training.
