I started to poke at Keras which is a high-level neural networks library, written in Python.  I used Keras with Tensorflow in the backend.
First, let import the Sequential model type from Keras.  This is simply a linear stack of neural network layers.

    from keras.model import Sequential
    from keras.model import Dense, Dropout, Activation
    
I impose constraint on weight for each hidden layer to make sure maximum norm of weight does not exceed value of 3
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
    
dropout is a regularization method for neural net
The dropout rate of 20% or one in 5 inputs will be randomly excluded from each update cycle.
I use categorical crossentropy for the loss, and sgd as the optimizer

    sgd = SGD(lr=0.1, momentum=0.9, decay=0.0, nesterov=True)
    model.compile(loss='categorical_crossentropy', optimizer='sgd')
