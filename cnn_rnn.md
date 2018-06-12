# cnn + rnn 
```
model = Sequential()
model.add(Embedding(1836, 128, input_length=1836))
model.add(Dropout(0.2))
model.add(Conv1D(64, 5, activation='relu'))
model.add(MaxPooling1D(pool_size=4))
model.add(LSTM(128))
model.add(Dense(3346, activation='sigmoid'))
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
model.fit(dtm_tf_test_a, one_hot_labels, validation_split=0.5, epochs=3)
```
