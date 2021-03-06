## BME 595A Deep Learning: Homework 6 Report

### Arindam Bhanja Chowdhury

##### Platform and Packages used:
Anaconda 4.3, python 3.6, PyTorch.
Operating System:   Ubuntu 14.04.
PyCharm IDE.

#### Overview of the code:
The objective of this assignment is to use the already trained **AlexNet** ([AlexNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)) convolution neural network and use it as a pretrained model to train a network to identify the images of the **Tiny ImageNet** dataset [Tiny ImageNet](https://tiny-imagenet.herokuapp.com/). Tiny Imagenet has **200** classes. Each class has **500** training images, **50** validation images, and **50** test images. Each of these images are **64x64** pixels in size.
The only difference between this model and the original AlexNet is that our model has only **200** nodes in the final layer instead of the **4096** nodes in the original AlexNet.
However, since AlexNet only accepts **224x224** images as inputs, so while creating the training and validation datasets, the 64x64 images of the Tiny ImageNet dataset are stretched and resized to 224x224 before feeding into the network.
There are two separate python scripts **train.py** and **test.py** for training and testing the code.
The train.py script copies all the pretrained layers from the AlexNet model except the final layer and then creates a train and validation loader of the images from the Tiny Imagenet dataset (downloaded) and used those to train the final layer of out network. The final trained model is saved by this script in a given location (may be the current directory).
The test.py script loads the model from that location.
We have also used a **cam** function for this assignment (just like the previous one). The test.py script actually runs the cam function.
The cam function captures the video from a camera and shows the video. This function also internally calls the forward function of the network and feeds it with a **64x64** resized version of every video frame (which is actually of **640x480** size). If a picture of an object that the network has been trained with is held in front of the camera, then the predicted object name is displayed on the screen.

#### How to run the code:
The **train.py** script can be run using the following command:
```
python3 train.py --data </tiny/imagenet/dir/> --save </dir/to/save/model/>
```
`</tiny/imagenet/dir/>` is the directory in which the Tiny ImageNet dataset is present (in unzipped format).
`</dir/to/save/model/>` is the directory in which the trained model is saved.

The **test.py** script can be run using the following command:
```
python3 test.py --model </dir/containing/model/>
```
`</dir/containing/model/>` is the directory from which the trained model is loaded. This is generally the same directory in which the model was previously stored.

#### Results on Tiny ImageNet Dataset:

| Model attributes | Modified ALexNet |
|:---:|:---:|
| **Training error (after 4 iterations)** | 5.000 |
| **Validation error (after 4 iterations)** | 4.905 |
| **Training Accuracy (%) (after 1 iterations)** | 27.61 |
| **Validation Accuracy (%) (after 1 iterations)** | 37.10 |
| **Training Accuracy (%) (after 4 iterations)** | 30.89 |
| **Validation Accuracy (%) (after 4 iterations)** | 40.31 |
| **Learning rate (eta)** | 0.001 |

#### Actual outputs of the status of training in the terminal:
```
 ########## ----------  [[   main: AlexNet   ]]  ---------- ########## 


Train Epoch: 1  [100000/100000 (100%)]      Loss: 5.039676
Training error: 5.035   Training Accuracy: 27.61 %  Validation Error: 4.939     Validation Accuracy: 37.10 %    Training time for current epoch: 5423.576 sec

Train Epoch: 2  [100000/100000 (100%)]      Loss: 4.996717
Training error: 5.024   Training Accuracy: 28.54 %  Validation Error: 4.925     Validation Accuracy: 38.43 %    Training time for current epoch: 11125.444 sec

Train Epoch: 3  [100000/100000 (100%)]      Loss: 5.003526
Training error: 5.014   Training Accuracy: 29.48 %  Validation Error: 4.920     Validation Accuracy: 38.87 %    Training time for current epoch: 16748.171 sec

Train Epoch: 4  [100000/100000 (100%)]      Loss: 5.006993
Training error: 5.001   Training Accuracy: 30.86 %  Validation Error: 4.912     Validation Accuracy: 39.81 %    Training time for current epoch: 27082.757 sec

Train Epoch: 5	[100000/100000 (100%)]  	Loss: 4.971263
Training error: 5.000 	Training Accuracy: 30.89 % 	Validation Error: 4.905 	Validation Accuracy: 40.31 % 	Training time for current epoch: 32015.660 sec

```
The name of this output file is [output_on_terminal.txt](https://github.com/abhanjac/BME-595A-Deep-Learning-Course/blob/master/abhanjac_HW06/output_on_terminal.txt).

#### Comments and Observations:
* Even though the model is pretrained, it takes a huge amount of time to train the last layer of the model on a laptop with CPU. 1 training epoch takes about 1 hour to complete.
* This is why we have not used more than 4 epochs. However the error seem to have a steady decreasing trend and the accuracy is also increasing with the iterations. Which indicates that the algorithm is getting trained.


##### Working of the cam function after AlexNet has been trained on Tiny ImageNet dataset:
![cam_function_output_cropped.png](https://github.com/abhanjac/BME-595A-Deep-Learning-Course/blob/master/abhanjac_HW06/cam_function_output_cropped.png)

