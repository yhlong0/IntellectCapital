# Deep Learning with Python

1. Linear regress -> Kernel Methods, support vector machine, kernel trick, kernel function. -> Decision trees, random forests, and gradient boosting machines -> Neural Networks ->
2. Support vector machine proved hard to scale to large datasets and didn't provide good results for perceptual problems such as image classification.
3. Gradient boosting machines: much like random forest, based on ensembling, iterativelly training new models that addressing the weak points of the previous model. It may be one of the best, if not the best, algorithm for dealing with nonperceptual data today.
4. Before 2010, neural network is not popular at all, 2011 Dan Cireasan win image-classification competitions with GPU-trained deep neural networks. 2011 the top-five accuracy of the winning model for ImageNet challenge was only 74.3%. Then 2012 CNN reach 83.6%, 2015 reached 96.4%. The classification task on ImageNet was considered to be a completely solved problem.
5. Deep learning not perform well, it also makes problem-solving much easier, it completely automates the crucial step *feature engineering*
6. Why deep learning thrive now? 
    1. Hardware: gaming market subsidized supercomputing/GPU for AI application.
    2. Datasets: internet make more data and data is easy to get.  
    3. Algorithmic advances:
        1. Better activation functions for neural layers
        2. Better weight-initialization schemes
        3. Better optimization schemes, such as RMSProp and Adam
7. Tensor is a container for data, almost always numerical data. 
    1. Number of axes(rank), matrix has two axes, ndim
    2. Shape, describes how many dimensions the tensor has along each axis, scalar -> (), matrix -> (3, 5), 3D -> (3, 3, 5)
    3. Data type, float32, uint8, float 64
    4. Housing data, Vector data, 2D, (samples, features), (1000, 3), 1000 housing data，every data has three features, bedroom, bathroom, price
    5. Image data, 4D, (samples, height, width, channels), (500, 28, 28, 3), 500 images, 28 pixels, RGB -> [Red 200, Green 100, Blue 75]
9. **Convolutional layers**(feature extraction, local pattern) -> Pooling layers(down sampling) -> Flatten layer(3D to 1D) -> Dense layer(s)(classifier)
10. Convolutional Layers:
    - The first layer acts as a collection of various edge detectors, the activations retain almost all of the information present in the initial picture.
    - As you go higher, the activations become increasingly abstract and less visually interpretable. They begin to encode higher level concepts such as "Cat ear" and "cat eye". It carry less information about the visual contents of the image, and increasingly more information related to the class of the image. 
    - The sparsity(scattered, thinly dispersed) of the activations increases with the depth of the layer, in the first layer, all filters are activated, but in the following layers more and more filters are blank.
13. **Pooling layers**(Max pooling / average pooling): 
     - Dimensionality reduction, reduce spatial dimensions, reduce the computational cost. particularly useful in deep networks with many layers. 
     - Can provide a form of translation invariance, robust to small changes or shifts in the input image.
     - Providing a form of abstraction of the input, prevent overfitting, regularization. 
14. **Flatten layer**: convolution and pooling layers output is a 3D tensor(height, width, channels), but the dense layers expect input in one dimension(a vector). The flatten layer is used to transition between these two parts of the network, reshapes the 3D output tensor into a 1D tensor.
15. **Dense layer**: use features from convolutional and pooling layers to perform actual classification. Learn global patterns, patterns involving all pixels. Each neuron in a dense layers has fully connected to previous layer, which is why they also known as fully connected layers. Several dense layer continues the pattern recognition task, the final dense layer often equals the number of target classes. 
16. When you design your layer, you need to consider the number of output class, each layer can only access information present in the output of the previous layer. If one layer drops some information relevant to the classification problem, this information can never be recovered by later layers(onformation bottleneck).
17. Training a convnet from scratch on a small dataset(base line) -> add more data -> regularization -> data/image augmentation -> transfer learning. It would prove difficult to go higher accuracy(85%+) just by training your own convnet from scratch. because you have so little data to work with. 
18. Use a ImageNet model(animals, daily objects) and then repurpose this for identifying furniture items in images, Such portability of learned features across different problems is a key advantage of deep learning compared to many older, shallow-learning approaches, and it makes deep learning very effective for small-data problems. 
19. VGG16(Visual Geometry Group) developed by Karen Simonyan and Andrew Zisserman in 2014. Multiple smaller filters(3x3) in consecutive stages, capture more complex structures. But VGG models can be quite heavy and slow, use a lot of computational resources during the training.
20. ResNet(Residual Networks): Microsoft Research, introduces the concept of "skip connections" or "shortcut connections", allow gradient to be directly backpropagated to earlier layers. Solved vanishing gradient problem, allow hundreds of layers deep. 
21. Inception(GoogLeNet): main innovation is the "Inception module" that applies multiple filter sizes on the same level, then concatenates the result. Allow model to handle different scales of features effectively, however can be more complex and harder to design due to their many hyperparameters. 
22.  Inception-ResNet: hybrid architecture that combines best features of Inception and ResNet, powerful architecutre that's both efficient and effective.
23.  Xception: Extreme Inception, Francois Chollet, the creator of Keras, depthwise separable convolution, where the spatial and channel-wise correlations in the data are mapped separately. A much lighter and faster model than Inception, with similar or even better performance. 
24. If your new dataset differes a lot from the dataset on which the original model was trained, you maybe btter of using only the first few layers of the model to do feature extraction, rather than using the entire convolutional base. 
25. Fine-tuning consists of unfreezing a few of the top layers of a frozen model base used for feature extraction, and jointly training both the newly added part of the model(fully connected classifier).It slightly adjusts the more abstract representations of the model being reused, in order to make them more relevant for the probelm at hand. 
26. Earlier layers in the convolutional base encode more-generic, reusable features, whereas layers higher up encode more-specialized features. It's more useful to fine-tune the specialized features, because these are the ones that need to be repurposed on your new problem. 
27. The more parameters you're training, the more you're at risk of overfitting. The convolutional base has 15 million parameters, so it would be risky to attempt to train it on your small dataset. 
28. 
29. Unsupervised learning is the bread and butter of data analytics, and it's often a necessary step in better understanding a dataset before attempting to solve a supervised-learning problem. Dimensionality reduction and clustering are well-known categories of unsupervised learning.
30. Self-supervised learning: supervised learning without human-annotated labels, without any humans in the loop, using heuristic algorithm. For example, Autoencoder given past frames, trying to predict the next frame, or the next word in a text. The distinction between supervised, self-supervised, and unsupervised learning can be blurry sometimes.
31. Reinforcement learning: an agent receives information about its environment and learns to choose actions that will maximize some reward. For instance, a neural network that looks at a video game screen and outputs game actions in order to maximize its score can be trained via reinforcement learning. 
32. If you expecting missing values in the test data, but the network was trained on data without any missing values, the network won't have learned to ignore missing values! In this situation, you should artificially generate training samples with missing entries: copy some training samples and drop some of the features that you expect are likely to be missing in the test data.
33. Calculate the model capacity by layers * filters(ask chatgpt for detail calculation) to get a trainable parameters. Compare this with training set to know if you are overfit. 
34. Small network starts overfitting later than powerful network, and its performance(loss validation) degrades more slowly once it starts overfiting(degrades after more epochs).
35. Dropout: inspired by a fraud-prevention mechanism used by banks, the tellers kept changing or got moved around a lot, this avoid cooperation between employees to fraud the bank, randomly removing a different subset of neurons on each example would prevent conspiracies and thus reduce overfitting. Introducing noise in the output values of a layer can break up happenstance patterns that aren't significant, which the network will start memorizing if no noise is present. 
36. When you see that the model's performance on the validation data begins to degrade, you've achieved overfiting. 
37. 
38. page 206
39. page 
