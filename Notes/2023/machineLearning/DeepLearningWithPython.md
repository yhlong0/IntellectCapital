# Deep Learning with Python

1. Linear regress -> Kernel Methods, support vector machine, kernel trick, kernel function. -> Decision trees, random forests, and gradient boosting machines -> Neural Networks ->
2. Support vector machine proved hard to scale to large datasets and didn't provide good results for perceptual problems such as image classification.
3. Gradient boosting machines: much like random forest, based on ensembling, iterativelly training new models that addressing the weak points of the previous model. It may be one of the best, if not the best, algorithm for dealing with nonperceptual data today.
4. Before 2010, neural network is not popular at all, 2011 Dan Cireasan win image-classification competitions with GPU-trained deep neural networks. 2011 the top-five accuracy of the winning model for ImageNet challenge was only 74.3%. Then 2012 CNN reach 83.6%, 20115 reached 96.4%. The classification task on ImageNet was considered to be a completely solved problem.
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
9. When you design your layer, you need to consider the number of output class, each layer can only access information present in the output of the previous layer. If one layer drops some information relevant to the classification problem, this information can never be recovered by later layers(onformation bottleneck).
10. Unsupervised learning is the bread and butter of data analytics, and it's often a necessary step in better understanding a dataset before attempting to solve a supervised-learning problem. Dimensionality reduction and clustering are well-known categories of unsupervised learning.
11. Self-supervised learning: supervised learning without human-annotated labels, without any humans in the loop, using heuristic algorithm. For example, Autoencoder given past frames, trying to predict the next frame, or the next word in a text. The distinction between supervised, self-supervised, and unsupervised learning can be blurry sometimes.
12. Reinforcement learning: an agent receives information about its environment and learns to choose actions that will maximize some reward. For instance, a neural network that looks at a video game screen and outputs game actions in order to maximize its score can be trained via reinforcement learning. 
13. If you expecting missing values in the test data, but the network was trained on data without any missing values, the network won't have learned to ignore missing values! In this situation, you should artificially generate training samples with missing entries: copy some training samples and drop some of the features that you expect are likely to be missing in the test data.
14. Calculate the model capacity by layers * filters(ask chatgpt for detail calculation) to get a trainable parameters. Compare this with training set to know if you are overfit. 
15. Small network starts overfitting later than powerful network, and its performance(loss validation) degrades more slowly once it starts overfiting(degrades after more epochs).
16. Dropout: inspired by a fraud-prevention mechanism used by banks, the tellers kept changing or got moved around a lot, this avoid cooperation between employees to fraud the bank, randomly removing a different subset of neurons on each example would prevent conspiracies and thus reduce overfitting. Introducing noise in the output values of a layer can break up happenstance patterns that aren't significant, which the network will start memorizing if no noise is present. 
17. When you see that the model's performance on the validation data begins to degrade, you've achieved overfiting. 
18. 
19. page 144
20. page 164
