I started to poke at Keras which is a high-level neural networks library, written in Python.  I used Keras with Tensorflow in the backend.
First, let import the Sequential model type from Keras.  This is simply a linear stack of neural network layers.

    from keras.model import Sequential
    from keras.model import Dense, Dropout, Activation
    
I apply Neural Net to NMIST dataset.  This is developed by Yann LeCunn, Corinna Cortes and Christopher Burges for evaluating
machine learning models on handwritten digit classification problem. Images of digits were taken from varieties of scanned documents
Each image is a 28x28 pixel square (or 784 pixels todal).  There are 10 digits (0 to 9) or 10 classes to predict.

The pixels are grey scale between 0 and 255.  For neural net, it is always a good idea to pre-process data by 
dividing by maximum to normalize data, and to center the mean at zero.

To start, I impose constraint on weight for each hidden layer to make sure maximum norm of weight does not exceed value of 3.
This is done using W_constraint = maxnorm(3)
    
    model = Sequential()
    model.add(Dense(128, input_dim=input_dim, init='normal', W_constraint=maxnorm(3)))
    model.add(Activation('relu'))
    model.add(Dropout(0.20))
    model.add(Dense(128, init='normal', W_constraint=maxnorm(3)))
    model.add(Activation('relu'))
    model.add(Dropout(0.20))
    model.add(Dense(nb_classes))
    model.add(Activation('softmax'))
    
Dropout is a regularization method for neural net
The dropout rate of 20% or one in 5 inputs will be randomly excluded from each update cycle.
I use categorical crossentropy for the loss, and sgd as the optimizer

    sgd = SGD(lr=0.1, momentum=0.9, decay=0.0, nesterov=True)
    model.compile(loss='categorical_crossentropy', optimizer='sgd')

There are several parameters that can be tuned to optimize prediction accuracies

    Start with Dense = 128 and a low learning rate of 0.01
    Increase momentum gradually from 0.8 to 0.9 
    Increase learning rate to 0.1
    Set nesterov=True
    Increase Dense to 512
