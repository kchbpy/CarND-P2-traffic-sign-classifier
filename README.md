**Traffic Sign Recognition** 


---



[//]: # (Image References)

[image1]: ./images/bar.png "bar chart"
[image2]: ./images/1_.jpg 
[image3]: ./images/2_.jpg
[image4]: ./images/3_.jpg
[image5]: ./images/4_.jpg
[image6]: ./images/5_.jpg
[image7]: ./images/view.png "conv1 visualization"


**Data Set Summary & Exploration**


I used the numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43


Here is an exploratory visualization of the data set. It is a bar chart showing how the data distribute in different labels

![alt text][image1]

**Design and Test a Model Architecture**

1. How I preprocessed the image data  

I did't preprocess the image data(like convert the images to grayscale) because I think the color contains some information.  

So i just normalized the image data to make
the data has mean zero and equal variance.





2. Final model architecture

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 3x3    	| 1x1 stride, valid padding, outputs 30x30x100 	|
| RELU					|												|
| Max pooling 2x2	   	| 2x2 stride,  outputs 15x15x100 				|
| Convolution 4x4    	| 1x1 stride, valid padding, outputs 12x12x150 	|
| RELU					|												|
| Max pooling 2x2	    | 2x2 stride,  outputs 6x6x150 		    	    |
| Convolution 3x3    	| 1x1 stride, valid padding, outputs 4x4x200 	|
| RELU					|												|
| Max pooling 2x2	    | 2x2 stride,  outputs 2x2x200 		    	    |
| flatten				|												|
| Fully connected		| outputs 200        							|
| Fully connected		| outputs 100        							|
| Fully connected		| outputs 43        							|
|||
 


3. Describe how you trained your model.  

My hyperparameters show in the table below  

|parameter              |value                                          |  
|:---------------------:|:---------------------------------------------:| 
|Batch                  |150                                            |  
|Epochs                 |20                                             |  
|Learning rate          |0.001                                          |  

In reference to the LeNet, I set the learning rate to 0.001.  


4. The approach taken for finding a solution  

My final model results were:
* training set accuracy of 0.940
* validation set accuracy of 0.954 
* test set accuracy of 0.940

At first I just using the LeNet(I learned on last lesson) but it can't make the accuracy greater than 0.93.
The traffic sign is more complex than handwriting.I think I should increase the depth of the LeNet.So I add one convolutional layer.The I adjust the width of each layer.

 

**Test a Model on New Images**

1. Five German traffic signs found on the web  

Here are five German traffic signs that I found on the web:

![alt text][image2] ![alt text][image3] ![alt text][image4] 
![alt text][image5] ![alt text][image6]

The third image might be difficult to classify because it's lack of some parts.

2. Model's predictions on these new traffic signs 

Here are the results of the prediction:  

| Image			        | Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road work      		| Road work   									| 
| Speed limit (30km/h)	| Speed limit (30km/h) 							|
| Stop					| Stop											|
| Turn right ahead	    | Turn right ahead					 		    |
| General caution		| General caution      							|

The model was able to correctly guess 5 of the 5 traffic signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 94.6%,is more accurate.

3. The softmax probabilities for each prediction  

For the first image, the top five soft max probabilities were  

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .9999         		| Road work   									| 
| 1.4e-5     			| Dangerous curve to the right				    |
| 4.6e-7				| No passing for vehicles over 3.5 metric tons	|
| 6.3e-8	      		| Speed limit (80km/h)          	            |
| 2.9e-10				| Bumpy road						            |

For the second image, the top five soft max probabilities were  

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .9999         		| Speed limit (30km/h)   						| 
| 1e-7     				| Stop										    |
| 2.2e-8				| Speed limit (100km/h)					        |
| 3.9e-10	      		| Speed limit (80km/h) 				            |
| 9.4e-11			    | Vehicles over 3.5 metric tons prohibited      |

For the thrid image, the top five soft max probabilities were  

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .88         			| Stop   									    | 
| 0.09     				| Speed limit (20km/h)				            |
| 0.025					| Pedestrians									|
| 2.8e-4	      		| Go straight or right	 				        |
| 1.5e-4			    | Speed limit (80km/h)				            |

For the fourth image, the top five soft max probabilities were  

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1         			| Turn right ahead   							| 
| 2.1e-13     			| Road narrows on the right 			       	|
| 1.5e-13				| Ahead only									|
| 6.1e-14	      		| Go straight or left    				        |
| 6.2e-15				| Dangerous curve to the left		            |

For the fifth image, the top five soft max probabilities were  

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1         			| General caution   							| 
| 7.2e-25     			| Traffic signals							    |
| 1.5e-26				| Bicycles crossing								|
| 1.1e-29	      		| Wild animals crossing	 				        |
| 2.2e-30				| Speed limit (30km/h)      		            |

 **Visualizing the Neural Network**  

The visualization of my first layer shown below.  
From the image we can find some features are detected by the model, like the shape of the traffic sign(featureMap21 featureMap22), the exclamation symble in the middle(featureMap44).So the model learned to detect useful features on its own.
![alt text][image7]

