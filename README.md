# NN-SMILES
### Neural Network Simplified model-input line-entry system

NN-SMILES is based on [SMILES](https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system), a notation for unambiguously describing molecular structure in serial format. 

What are molecules if not [graphs](https://en.wikipedia.org/wiki/Molecular_graph)? NN-SMILES applies the same approach to describing deep neural networks. 

For example, a simple image classifier might be: 

`I(CRP)3ddO `
 - I = input
 - C = convo 2D 
 - r = ReLU
 - P = max pooling 2D
 - d = dense (fully connected)
 - O = output
 
Upper case would be 2D, lowercase 1D or flat. The problem is, there is more information to encode than just the type of layer. We also need to know the number of nodes, and for things like convo layers, the kernel size. 

`I(C3,3,64rP2,2)3d128d10O `

A little ugly, but still fairly succinct. 

Since maintaining the same tensor volume through pooling operations (e.g. MaxPool(2,2) usually results in a 4x increase in number of filters of the next convonet), we could also have a notation to indicate this typical operation. 

I64,64(C64,3,3,r)[2,2]>3d128d10O

would be
- Input(64,64)
- Convo(3,3) with 64 filters, ReLU, and MaxPool(2,2), output shape=32x32
- Convo(3,3) with 256 filters, ReLU, and MaxPool(2,2), output shape=16x16
- Convo(3,3) with 1024 filters, ReLU, and MaxPool(2,2), output shape=8x8
- Dense(128)
- Dense(10)
- Output

Might need a more compact way of representing activation functions. 

Proposed symbols: 
- C - ND convo, filters first - C64,3 1D w/ 64 filters, C64,3,3 2D, C64,3,3,3 3D etc
- P - Pm (max)pooling, Pa (average)pooling - P2 1D pooling, P2,2 2D pooling (2x2)
- d or . - densely connected
- r or R or / - ReLU
- s or $ - sigmoid
- L - LSTM
- G - GRU
- # - Time-distributed dense
- z - Variational latent layer
- [m,n]> - Pooling (as part of multiple convolution and downsample operations)
- [m,n]< - Upsampling

Still need to figure out more exotic RNNs and ResNets, but since the SMILES notation is designed to handle cyclic graphs, this should be pretty straightforward. 
