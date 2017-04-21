# NN-SMILES
### Neural Network Simplified model-input line-entry system

NN-SMILES is based on [SMILES](https://en.wikipedia.org/wiki/Simplified_molecular-input_line-entry_system), a notation for unambiguously describing molecular structure in serial format. 

What are molecules if not [graphs](https://en.wikipedia.org/wiki/Molecular_graph)? NN-SMILES applies the same approach to describing deep neural networks. 

For example, a simple image classifier might be: 
I(CRP)3ddO 
 - I = input
 - C = convo 2D 
 - R = ReLU
 - P = max pooling 2D
 - d = dense (fully connected)
 - O = output
 
Upper case would be 2D, lowercase 1D or flat. The problem is, there is more information to encode than just the type of layer. We also need to know the number of nodes, and for things like convo layers, the kernel size. 
I(C3,3,64RP2,2)3ddO 

A little ugly, but still fairly succinct. 
