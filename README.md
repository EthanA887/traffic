# Experimentation Process for Traffic

---

### Part 1: load-data() function

For the first function in this AI, I started working backwards. The specification required a return value of the tuple `(images, labels)`, so first, I initialized the two arrays. Then, looping through each image in each folder of the dataset, I used `cv2.imread` from the OpenCV Python module to load an image and save it as a variable called `image`, also parsing the file name with `os.path.join`. Next, the image was resized to a 30x30 array and appended to `images`. The folder's name was also appended to `labels` with `os.path.join`. 

### Part 2: get-model() function

This function needed the most experimentation and debugging. I decided to use the `tf.keras` module to build my neural network, so I started reading its documentation. After importing everything from the module, I started with a for loop of three convolutional layers and three pooling layers. This immediately returned an error, stating that I had a negative dimension size due to the arguments in `tf.keras.Conv2D` and `tf.keras.MaxPooling2D`. I found the root of the error, in MaxPooling2D, where I changed the filter size from (6, 6) to (2, 2) and made an extremely simple neural network with just two layers (one convolutional and one pooling). Finally, the negative dimension error was resolved and I was ready for the first stages of testing my program. On the first test, my neural network ended with 4% accuracy after ten epochs. To get a decent accuracy percentage, I restored the structure of three convolutional and three pooling layers, this time with a lower number of filters so as to avoid another error. This testing stage ended with 80% accuracy after ten epochs. I knew there was still room for improvement, so I decided to play around with the types of layers and activation functions. I switched the convolution layers' activations from a basic step function to a sigmoid. There wasn't much of a change in accuracy, so I tried something else. Instead of having convolution and pooling layers, I used the function `tf.keras.layers.Dense` to create five hidden layers in the neural network, each one with 128 units and a ReLU (Rectified Linear Unit) activation. The test ended with 92% accuracy, and I noticed by the third epoch, the network was already trained up to 80% accuracy. My next and final experiment was to add another hidden layer of the same structure, and the completed neural network ended with a whopping 96% accuracy.
 
###### Created by Ethan Ali
