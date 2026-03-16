2025.01.11 - 01.15

Attention Is All You Need - https://arxiv.org/abs/1706.03762

Original paradime was RNN(Encoder-Decoder) - supportive Attention - CNN
 RNN assumes language must be done in sequence -> close to no parallelization [sequence via time step - many hidden states, bad long-term, bad parallel]
 CNN focuses on local patterns [Read via window - considers local patterns, combine via layer stacking, better long dependency and allows parallelization though less than Transformer]

Transformer ditches the sequence and instead does Positional Encoding, relys heavily on Attention (Multiheaded Self-Attention).
 While computation complexity is higher than RNN(n) and CNN(nk) as n^2, its faster via full paralleization by not needing time-steps at all.

 Positional Encoding : the sequence is encoded as placement info rather than being handled by the structure
  After the token is turned to vector, the positional encoding(vector that represents the position) is simply added. Not used in attention.
  Change of this can differ transformers interpretation -> leads to RelativePE / RoPE / ALiBi

 Self-Attention : sees all token as a node of a fully connected graph, connected by attention score as edge weight.
  doesn't care about positions - sees relationship regardless of position, leading to a more accurate relationship learning.
  Multi-head to show multiple relation types


*Personal Notes*
In short, Transformers seperated the sequence info from the structure into its embedding.
This allowed 1) a more flexible architecture with full parallelization
             2) learning token relationships without enforcing sequential rules - leading to higher accuracy and better modeling of long-range dependencies