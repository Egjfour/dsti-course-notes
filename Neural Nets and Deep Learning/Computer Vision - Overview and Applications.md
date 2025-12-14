|    Course Name    |      Topic      |   Professor   |       Date       |       Tags       |
| :---------------: | :-------------: | :-----------: | :--------------: | :--------------: |
| **Deep Learning** | Computer Vision | Benoit Mialet | 01 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251201%5F095003%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E738091b4%2Db88f%2D4216%2D99be%2D18175483b0d6)

# Summary
*Computer vision allows AI models to interpret visual information stored as 3D tensors. These models are useful for a variety of tasks and applications such as medical diagnostics, self-driving cars, and automatic image captioning. Many model architectures have been proposed and improved over time, but the key advancement was the ImageNet project to hand-classify millions of images to train computer vision models.*

# Key Takeaways
1. In practice, most computer vision applications are a blend of several tasks
2. Computer vision inputs are images, videos, and/or multi-channel signals (RGB, depth, ...)
3. Computer vision can be done on streams though this is much more difficult
4. The Intersection-Over-Union metric measures the quality of bounding boxes

# Definitions
- Computer Vision: A field of AI that enables computers to understand and interpret visual information
	- Self-driving cars, facial recognition, etc
- Image Classification: Predict one label from one image
	- ResNet, AlexNet
- Object Classification: Locate and classify multiple objects within an image including their bounding boxes
	- Yolo, Faster R-CNN
- Semantic Segmentation: Assign a class label to each pixel
	- U-Net, DeepLab, Segment Anything
- Instance Segmentation: Distinguish between individual instances of the same class (multiple people in an image)
- Bounding Box (bbox): Localisation of each object using 4 coordinates (x1, y1, x2, y2)

# Additional Resources
- [YOLO Video](https://www.youtube.com/watch?v=G7oGWh8PZAE)

# Notes
## Computer Vision Task Types
- Image classification
	- Dog vs cat
- Object detection
	 ![[Pasted image 20251213134121.png]]
- Semantic segmentation
	 ![[Pasted image 20251213134147.png]]
- Instance segmentation
	 ![[Pasted image 20251213134215.png]]
- Pose estimation: Detect position of key body parts/joints (MMPose)
	 ![[Pasted image 20251213134251.png]]
- Depth Estimation: Predict distance/depth for each pixel (MiDaS)
	 ![[Pasted image 20251213134355.png]]
- Optical Flow Estimation: Motion of pixels between video frames
	- Generative predictions possible
- Other generative tasks
	- Image captioning (CLOP+GPT2)
	- Image Generation from prompt (Stable diffusion/DALL-E)
	- Image Enhancement: Improve quality/resolution (SRGAN)
## Primary Applications and Key Advances
- Applications
	- Medical diagnostics
	- Agriculture
	- Self-driving cars
- Timeline
	- Hubel and Wiesel in 1959 demonstrated that lower-level neurons interpret visual stimulus and pass this information to more integrative neurons
	- Early form of the [[Convolutional Neural Networks|CNN]] proposed bu Fukushima in 1980 (NeoCognition)
		- Had manual tuning by hand which was revolutionized by [[The Training Process|backpropagation]] from Hinton in 1986
		- LeNet in 1998 applied [[Gradient Descent and Optimizers|stochastic gradient descent]] to NeoCognition
	- ImageNet project launched in 2009 to solve the lack of data issue
	- Hinton leveraged ImageNet to create AlexNet in 2012 leading to the explosion of deep learning
## Main Models by Task
- Image Classification
	- LeNet: first successful CNN
	- AlexNet
		- Applied [[Evaluation of ML Models & Improving Results|dropout]] and heavy data augmentation
	- VGG: Showed "deeper is better" for CNNs
	- ResNet: Solved vanishing gradient problem for very deep networks with Kaiming weights initialization and skip connections
		- Widely used today
- Semantic Segmentation
	- Creates a 2D map the same size as the input
	- Cannot use classic ConvNet because there is no global image understanding
	- Fully Convolutional Networks (FCN) use 1x1 convolutions instead of fully-connected layers
		- Size is constant from input to output image
	- U-Net used an autoencoder strategy to make FCN less computationally expensive
		 ![[Pasted image 20251213135955.png]]
- Object classification
	- Goal is to output both a classification and bounding box
	- Uses two losses (categorical and MAE) simultaneously
	 ![[Pasted image 20251213140230.png]]
	- Main issue is region proposal, so combining region-based and CNN approaches was necessary
		- Still slow, so SOTA models are Fast R-CNN, Faster R-CNN, and Mask R-CNN
		 ![[Pasted image 20251213140407.png]]
	- These models can be evaluated using the IoU metric
		- Area of bbox intersection between ground truth and predicted divided by bbox union