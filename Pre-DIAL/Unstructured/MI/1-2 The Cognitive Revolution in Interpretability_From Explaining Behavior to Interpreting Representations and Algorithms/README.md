2025.01.06 - 01.10

The Cognitive Revolution in Interpretability: From Explaining Behavior to Interpreting Representations and Algorithms - https://arxiv.org/abs/2408.05859

ML
1.Semantic interpretation(what latent representations are learned and used by models)

 A.Optimization and Search - what input maximize the activation of a given neuron
  Early works focus on finding patterns in image recognition networks -> Later adapted to language and multimodal
  -Levels of Representation : Polysemanticity, Different architecture consideration
  -No generally accepted methodology for determining which neurons are most important for any given analysis
 
 B.Structural Probing - assums "if a feature is assumable from the embedding the model is representing that" and uses a probe to find said features
 -Levels of Representation : architecture of probe - Linear[Linear subspace hypothesis(ex)results are linear), may underdeliver for non-linear info], Non-linear[expressive models, may overdeliver by learning the full learnt info not a single feature]
 -Possible failure to capture without a method of checking -> may lead to misleading results
 -Correlation isn't causation

 C.Causal Probing - intervention is performed over representations and resulting impact is measured, causal to solve B's problem
  -Same problem with B as to predefine level of representation and set of properties for which to probe before starting
  -Rashomon effect: if multiple explanations of equal causal efficiacy exists, there's no way to determine which is correct
  -Linear interventions are incomplete(may disprove linear subspace hypothesis) vs Non-linear interventions aren't selective enough that it may just cause the results be about the collateral damage instead.
 
 D.Dictionary Learning - train an unsupervised probe to decompose embeddings to a sparse combination of features, dictionary of features
  Sparse Auto-Encoders: nonlinear transformation of input embeddings onto an overcomplete linear basis via neural networks
  -Levels of Representation : Superposition hypothesis("models learn to represent more features than they have neuronsin a given layer by encoding by almost-orthogonal directions in embedding space")
  -Unsupervised Feature Interpretation -> SAE gets features without labels so it needs to be interpreted by humans individually, not viable for bigger scaled projects
  -Not clear how one should evaluate whether any given feature interpretation is correct.


2.Algorithmic interpretation(what operations are being implicitly implemented by models to carry out a given behavior)
 
 A.Circuit Discovery - intervene forward pass by (a)or(b) and study the effects
  a) Knockout : turn off a sub-circuit by nullifying it
  b) Patching : replace circuit outputs in the course of computing a target sequence with activations from computing a source sequence
  -Must decide on atomic sub-graph -> limit on results
  -Only process being done on a neuron or sub-graph isn't realistic
  -Pre-Specification : current circuit discovery is more so checking algorithms we already know
  -Rashomon Effect



Personal Key Notes
 A recap of 1-1 paper. Shows how this recent field has different views on how methods are to be sorted.