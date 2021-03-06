# What we did to improve the prediction (including limitations):
Change the activation function (bad idea - sigmoid is the only useful activation function, really)
- tried reLU, softPlus. Both were made by creating new functions in the sigmoid block.

Added 1,000 images from the CalTech training dataset
- We attempted to add more than 1,000 images, but colaboratory continued to crash due to a lack of RAM.
- At first, adding images to the training set seemed to make the model worse - the cost increased, and the training accuracy and test accuracy decreased.
- However, in order to take full advantage of the extra images, more iterations must be added. With 1,000 more iterations, the test accuracy increased, but the cost still remained higher than original and the training accuracy remained lower than the initial.
- We then increased the number of iterations to 10,000, which decreased the cost significantly and increased the test accuracy from 70% to 78%. For 10,000 iterations, overfitting occurred (see part 3b). 

Changing number of iterations
- An increase in iterations leads to a decrease in cost; of course, more iterations takes more time.
Changing the batch size
- We attempted to use a smaller batch size for each iteration, but we ran into errors that we could not figure out with the indexing and concatenation of the X and Y arrays.

Mess with learning rate (jumping around in the parabola)
- The larger the learning rate, the worse it got
- But if it was too small…
- leads to “overfitting”.
- When overfitting occurs, the model is overtraining for the training set and then ends up being less accurate for the testing set.
- Some values would “break” the code - potentially linked to the cost fxn

# derivative of cost function wrt w (scalar)
    dw = (1./num_images)*np.dot(X,((A-Y).T))
  
    To find the derivatives of the cost functions we will first look at the sigmoid function and divise that to dz/dphi = phi(phi-1) and then considerr z = x.w and divise this to get dphi/dWi = (dz/dphi)(dw/dz) = phi(phi-1)Xi    # To get our new dw we will use the equation: Wnew = Wold - n(dphi/dWi). The Wold being the old dw and the n being the number of images that are being run through. This will allow us to take smaller sections of the gradient descent of the curve and decrese the error.  
     derivative of cost function wrt b (scalar)
    
    db = (1./num_images)*np.sum(A-Y,axis=1)
  
     To find the derivative of the cost function db, it is very similar to that of dw. Though, the z changes for it is a sum of x and w and not a dot product. Thus, z = x + w and the db/dz = 2.    # #Though the dz/dphi will stay the same as that from dw. Thus dphi/dbi = (dz/dphi)(db/dz) = phi(phi-1)2. Then to get the final db we will get Bnew = Bold - n(dphi/dbi). 

# Discuss how image recognition is done by data scientists today.
TensorFlow: artificial intelligence software
- “Neural network:” operates in a way that mimics the human brain in learning and reasoning. End goal is for these networks to detect and interpret patterns/correlations
- Many, many, many layers of choices are applied to narrow down the characteristics of an image, for different objects in the image, compared to an entire database of already learned elements of different classified images.
- TensorFlow still operates with logistic regression - flattening, learning rate, weights, biases, etc. Multiple, defined operations (rather than just the one that we did for cat identification) take in a tensor (a multidimensional array) as an input, and output a tensor as well.
- TensorFlow can be “wrapped” in a nice interface that helps to visual the cost functions, variability in biases and weights with time, and graph the flow of tensors (hence TensorFlow) with graphs like the image below:
- Looks like TensorFlow uses softPlus - in retrospect this would have been a good one to try.

![alt text](https://www.techspot.com/images2/news/bigimage/2015/11/2015-11-09-image.gif)
