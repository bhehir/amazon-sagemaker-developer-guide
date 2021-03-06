# How Sequence2Sequence Works<a name="seq-2-seq-howitworks"></a>

Typically, a neural network for sequence\-to\-sequence modeling consists of a few layers, including: 

+ An embedding layer\. In this layer, the input matrix, which is input tokens encoded in a sparse way \(for example, one\-hot encoded\) are mapped to a dense feature layer\. This is required because a high\-dimensional feature vector is more capable of encoding information regarding a particular token \(word for text corpora\) than a simple one\-hot\-encoded vector\. It is also a standard practice to initialize this embedding layer with a pre\-trained word vector like [FastText](https://fasttext.cc/) or [Glove](https://nlp.stanford.edu/projects/glove/) or to initialize it randomly and learn the parameters during training\. 

+ An encoder layer\. After the input tokens are mapped into a high\-dimensional feature space, the sequence is passed through an encoder layer to compress all the information from the input embedding layer \(of the entire sequence\) into a fixed\-length feature vector\. Typically, an encoder are made of RNN\-type networks like long short\-term memory \(LSTM\) or gated recurrent units \(GRU\)\. \([ Colah's blog](http://colah.github.io/posts/2015-08-Understanding-LSTMs/) explains LSTM in a great detail\.\) 

+ A decoder layer\. The decoder layer takes this encoded feature vector and produces the output sequence of tokens\. This layer is also usually built with RNN architectures \(LSTM and GRU\)\. 

The whole model is trained jointly to maximize the probability of the target sequence given the source sequence\. This model was first introduced by Sutskever et al\. in 2014\. 

Attention mechanism\. The disadvantage of encoder\-decoder framework is that model performance decreases as and when the length of the source sequence increases because of the limit of how much information the fixed\-length encoded feature vector can contain\. To tackle this problem, in 2015, Bahdanau et al\. proposed the [attention mechanism](https://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf)\. In an attention mechanism, the decoder tries to find the location in the encoder sequence where the most important information could be located and uses that information and previously decoded words to predict the next token in the sequence\. 

For more in details, see the [paper](https://arxiv.org/abs/1508.04025) by Luong et al\. that explains and simplifies calculations for various attention mechanisms\. This [paper](https://arxiv.org/abs/1609.08144) by Google describes their architecture for machine translation, which uses skip connections between encoder and decoder layers\.