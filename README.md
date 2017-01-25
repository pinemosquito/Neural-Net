Keras is a high-level neural networks library, written in Python 
The core data structure of Keras is a model

from keras.models import Sequential
model = Sequential()

Layers are stacked using .add():

from keras.layers import Dense, Activation

model.add(Dense(output_dim=64, input_dim=100))

model.add(Activation('relu'))
model.add(Dense(output_dim=10))
model.add(Activation('softmax'))
