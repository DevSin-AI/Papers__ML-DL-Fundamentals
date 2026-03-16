2025.01.01 - 01.05

Unboxing the Black Box: Mechanistic Interpretability for Algorithmic Understanding of Neural Networks - https://arxiv.org/abs/2511.19265

Introduction
 Emergence of Importance of Explainable AI (XAI),
 Explainable(Explainable decisions) vs Interpretable(Interpretable innerworkings) vs Trustworthy(safe and ethical)
 Taxonomy - via normally Stage(Ante-hoc / Post-hoc - Model-agonistic & Model-specific), Scope(Local / Global). also Input data(Numerical, Categorical, Vectors), Output format(Numerical, Visual, Textual)
 Mechanistic Interpretability(MI) _ a 'post-hoc','model-specific' approach within XAI & reverse engineering on internal structure interpretability

Definition : study the inner computation of neural networks and translate to human-understandable algorithms
 Feature[interpretable properties encoded in neurons unit : traditionally input data attributes, seen as abstractions of internal properties in MI]
 Polysemanticity = phenomenon where single neuron encodes multiple features to accommodate limited neuron num, causes challenge to interpretation
 MI analyzes Circuits [minimal computational subgraphs of neural networks that are responsible for performing a given task, defined as directed acyclic graphs]
 Universality hypothesis [yet-to-be-proved-idea that similar circuits, features are present across tasks and models -> those patterns are called Motifs]
 Taxonomy via Scope(Neuron, Layer, Circuit), Task(Circuit discovery, Feature disentanglement, Feature localization), Nature(Observational, Interventional)

Feature Localization : characterize individual neurons (characteristics like Importance)
 Probing : probe(a simple classifier) supervised-learns generated representations to learn the process
  Sparse Probing - identify only the subset that's activated by input (Adaptive thresholding, Optimal sparse probing of Gurnee et al./ Ridge regression-based probes of Chowdhruy and Allan)
  Edge probing - assess if local token relationships are encoded within representation
  Structural probing - assess global hierarchical structure encoded within representation
 Lenses : rather than focusing solely on a specific state, maps representations from intermediate layers to the model's vocab distribution directly
  Logit Lens : map hidden state of a layer to the output vocabulary space by computing vocabulary logits ( multiplying hidden state with the output embedding)
  DecoderLens : extension of logit lens, propose enabling the decoder to cross-attend to intermediate encoder layer representations rather than relying soely on the final encoder output
  Linear Lens, Tuned Lens, Future Lens, Jailbreak Lens, Diffusion Lens, Semantic Lens, ...

Circuit Discovery : identify causal graphs of the network, main framework is based on CMA[Causal Mediation Analysis, use mediators(intermediate elements that influence final outcome) in analysis]
 Patching : also known as Interchange Intervention, intervene model components and observe changes to identify specific components that are causally responsible. [Causual Relationship]
  Activiation patching - find role of specific neuron in decision process by observing change in activations, Clean Run -> Corrupted Run -> Patched Run(specific parts of corrupted is replaced to clean's)
  Attribution patching - use a gradient-based approximation to find linear estimate between clean and corrupted pass rather than a forward pass for each substitution
  Path patching - constrains the interventions to a specific path of model, path(edge) instead of neuron(vertex)
 Ablation Study : remove or disable certain elements to identify which components are essential for functionality [Causual Importance]
  Removal => performed via Zero ablation(set value to 0), Mean ablation(set value to average),..
  Targeted edge ablation(focus on disabling edges responsible for bad behavior), Causal scrubbing(generalized approach of testing hypotheses of model behavior)

Feature Disentanglement : aims to resolve polysemanticity by enumberating all the features encoded by the network
 Based on Superposition hypothesis - polysemanticity results from compression of features in a limited representational space
 ad-hoc(design model without superposition)
  linear models that have no superposition, non-linear networks with reduced sparsity of features, increasing the number of neurons per layer, ...
  Being debated in terms of computational loss, performance and compacity being impacted by monosemanticity
 post-hoc(employ sparse coding to describe how features are represented in models with superposition)
  SAE(sparse autoencoders) : decompose entangled space to a sparse representation that allows independent analysis of features
  
Challenges
 Superposition, Polysemanticity
 Spurious correlations(can uncover mechanisms that rely on coincidental or non-causal patterns and be human-misinterpreted)
 Semantic drift(meaning of internal representations can shift across network layers or training checkpoints, challenge for longitudinal analyses)
 Pitfalls of intervention(intervention may influence model behavior, making causal importance of components uncertain)
 Evaluation problems(hard to get metrics for faithfulness, completeness, or usefulness)
 Deficit of automation, Scalability(require extensive manual work - not realistic for large complicated models)


Personal Key Notes
 Paper on what is MI, and the general landscape of the study. Good for understanding what MI is, not much opinions in or on it.
 While not completely seperable - MI(Mechanistic Interpretability) is but a part of the full family of methods on interpreting AI. However, methods like Behavioral post-hoc explanations lack in consideration of security compared to it. When considering AI interpretation in security wise - look for MI related papers.