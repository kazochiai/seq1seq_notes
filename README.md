Sequence to Sequence
  - chat bot (Many to many)
  - translation service (Many to many)
  - Summerization boot
  - Q & A

Recurrent Neural Network
  - Sequence of data any length. They share parameters across different time steps.
  - Map a sequence of any length to a sequence of any length
    - Use 2 RNNs. One that reads the sequence and the hands over what it had learned to another RNN
    which start outputting another output sequence.


Architectures
Input -> Encoder -(Context)-> Decoder -> Output


To Do's for Seq2Seq
Cornell Movie-Dialogs Corpus
https://www.cs.cornell.edu/~cristian/Cornell_Movie-Dialogs_Corpus.html

preprocessing of Cornell movie data set
use Data.py of chiphuyen.tf-stanford-tutorials
Take a look at the processed output and the data.py's code

Sequence to Sequence Model Excersise
- A model that takes in a sequence of letters, and outputs a sorted version of that sequence.

1. Preprocessing
  - Convert the characters to int
2.1 Encoder
  - Embedding
  - Encoder cell
2.2 Decoder
  1- process decoder inputs
  2- Set up the decoder
    - Embedding
    - Decoder cell
    - Dense output layer
    - Training decoder
    - Inference decoder
  2.3 Seq2seq model connecting the encoder and decoder
  2.4 Build the training graph hooking

2.1 Encoder
  -(Input)->[tf.contrib.laters.embed_sequence()]-(Embedded Data)->[a stack of RNN]-(Encoder_out, Encoder_state)->
2.2 Decoder
 - In the training process, the target sequences will be used in two different places:
  1. Using them to calculate the loss
  2. Feeding them to the decoder during training to make the model more robust.
    - tf.strided_slice() to preprocess tensor for feeding the decoder. Cut the last word since we don't need it.
    - The first item in each sequence we feed to the decoder has to be <GO> symbol
- Embedding
  Need to embed them so they can be ready to be passed to the decoder
- Decoder cell
   - tf.contrib.rnn.LSTMCell
   - Declare a decoder for the training process and inference/predection.
   These two decoders will share their parameters
- Dense output layer
  - tensorflow.python.layers.core.Dense layer
  - translates the outputs of the decoder to logits that tell us which element of the decoder vocabulary the decoder is choosing to output at each step
- Training decoder
  - tf.contrib.seq2seq.BasicDecoder
  - tf.contrib.seq2seq.dynamic_decode
  - We'll be creating two decoders which share their parameters. One for training
  and one for instance. They differ in that we feed the target sequences as inputs to the training decoder at each time step to make it more robust
