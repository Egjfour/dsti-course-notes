|    Course Name    |         Topic          |   Professor   |       Date       |       Tags       |
| :---------------: | :--------------------: | :-----------: | :--------------: | :--------------: |
| **Deep Learning** | Computer Vision - CNNs | Benoit Mialet | 01 décembre 2025 | #MachineLearning |

[Class Video Link](https://dstisas.sharepoint.com/sites/RecordingsArchive/_layouts/15/stream.aspx?id=%2Fsites%2FRecordingsArchive%2FShared%20Documents%2FA24%2FA24%20%2D%20Common%20Link%20DSDEDA%2D20251201%5F095003%2DMeeting%20Recording%2Emp4&ga=1&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E738091b4%2Db88f%2D4216%2D99be%2D18175483b0d6)

# Summary
*Convolutional neural networks are the solution to the problems faced by simple multilayer perceptrons when dealing with image data: translation invariance and massive memory needs. These models use a filter to interpret an image as smaller subsections of that image. Additional components are added as well such as pooling and stride to help improve the model's ability to understand global context of an image.*

# Key Takeaways
1. CNNs are used for [[Computer Vision - Overview and Applications|computer vision]] because [[Elements of a Neural Network|multilayer perceptrons]] fail to exploit translation invariance. CNNs, however, are translation invariant
2. The convolutional layer creates a 2-dimensional activation map
3. "What" is inside the CNN filters is directly a result of the model task and loss function
4. In object detection, a neuron cannot recognize large objects if the receptive field is too small
5. In classification, larger receptive fields capture global information and generally improve accuracy
6. The output size is equal to $(W - K + 2P)/S +1$

# Definitions
- Translation Invariance: An object can be recognized as itself even when the appearance varies in some way (e.g., relative positions for the camera/viewer)
	- A tree on the left or right side of an image is still a tree
- Convolution: Sliding over all locations of an image
- Receptive Field: The region in the input space that a particular CNN feature is looking at/can be affected by
- Stride: Skipping some pixels as the convolution filter moves across the image to increase the receptive field
- Pooling layer: Reduce the spatial size of a feature map while keeping the important information

# Additional Resources
- [What is translation invariance in computer vision](https://stats.stackexchange.com/questions/208936/what-is-translation-invariance-in-computer-vision-and-convolutional-neural-netwo)

# Notes
## Images as Input
- Recall, a neural network is only capable of processing numeric inputs
- Thus, we represent images as 3D tensors
	- Either 3 channels (RGB) or 1 channel (grayscale)
	- Usually the value of a pixel is between 0-255 though [[The Training Process|min-max scaling]] is often applied
	- The shape is `[batch size, # channels, image height, image width]`
## Convolution Layers
- An MLP would require that we flatten the image height and width to create a 1D vector
	- Each neuron would have to connect to each pixel which would scale poorly
	- This solution would also ignore spatial structure (no information for which pixels are neighbors)
- The solution - convolution layers
	- We create filters (kernels) which look at a small subset of the input image
		- These filters act as "templates" that we are trying to match
		- Each filter is a single MLP neuron
			- e.g., a dot product between the filter and small subset
	- These layers <mark style="background: #FFB86CA6;">significantly reduce the number of computations</mark> compared to an MLP
- The output of a convolution layer is a 2D activation map
	- This activation map is what introduces translation invariance
		- If the given template pattern is anywhere in the image, the kernel will find it
- Convolution can be extended to 1D and 3D spaces as well
 ![[Pasted image 20251214113539.png]]
## Convolutional Neural Networks
- A CNN (or ConvNet) is a feed-forward neural network used to analyze visual images
- Core elements
	- Repeated many times
		- Convolution Layers
			- Input of 3D images and 4D filters (since <mark style="background: #FFB86CA6;">we use many filters at once</mark>)
		- Activation (ReLU)
		- Pooling (Max/Average)
	- A Fully-Connected layer on the flattened final output of the repeated steps above
	- Softmax activation (presuming image classification)
- The size of the kernel is $Channel_{out} * Channel_{in} * Kernel_{width} * Kernel_{height}$
	- $Channel_{out}$ is the number of kernels we have
- The size of the output image is decreasing with layers
	- $size_{output} = W - K + 1$ (width - kernel size + 1)
	- To solve this, we pad the image with zeros
	- This also helps the model learn the pixels on the edge of the image better
	- The new size with padding is $size_{output} = W - K + 1 + 2P$ with $P$ the pad size
- The kernel size and image size directly affect the receptive field of the image
	- It is important to try to get this relatively large so that the features are processing large portions of the input image
	- This is why <mark style="background: #FFB86CA6;">later layers in the network process higher-level information</mark> since they can see more of the total input image
	![[Pasted image 20251214114904.png]]
	- To increase the receptive field without going quite as deep, stride is used
		- Useful when we want to increase the receptive field without increasing the memory footprint
		- With stride, the final activation map size is (W -K + 2P)/S + 1 with S as the stride
- A CNN <mark style="background: #FFB86CA6;">stacks multiple convolution layers</mark>
	- In general, filter size reduces but the number of channels increases as we go deeper
- The Pooling Layer
	- These are a <mark style="background: #FFB86CA6;">parameter-free way to reduce the spatial size</mark> of the feature map while preserving the important information
	- Act similar to filters but with no parameters
	- Mean and Max pooling are the two most common with <mark style="background: #FFB86CA6;">max pooling what is typically used</mark>
	- Pooling conserves the number of channels and is translation invariant
## CNN in [[Neural Networks in PyTorch - Overview|PyTorch]]
- Main utilities
	- Convolutional layers `torch.nn.conv2d(in_channel, out_channel, kernel_size)`
		- Note that you must calculate the in and out channels yourself
	- Pooling Layers
		- `nn.MaxPool2d` and `nn.AvgPool2d`
	- For the final MLP portion, we use `flatten`
		- Make sure to not flatten the batches. There should be one 1D tensor per batch element
