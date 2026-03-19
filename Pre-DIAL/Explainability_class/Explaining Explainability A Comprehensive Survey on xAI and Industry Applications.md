2026-03-16 ~ 2026-03-17

Title: Explaining explainability: A comprehensive survey on explainable artificial intelligence and relevant industry applications 
Topic: XAI
Link: https://www.sciencedirect.com/science/article/pii/S2667305326000220?ref=pdf_download&fr=RR-2&rr=9dd3fbd29c39ea74

============================================================
A. FIELD MAP
===
1) Field Definition
 Field dedicated to figuring out decision-making processes of AI systems that are currently a black-box for transparency, trust, accountability

2) Core Branches
 Interpretability
  Also happens to be or be in relation to post-hoc explainability tech;
    1.Model Simplification - Explainable surrogate model(LIME, GraphLIME), Rule setting to explain the original complex function(G-Rex)
    2.Feature Relevance - Sensitivity analysis(explain function via ranking input features according to importance/relevance for a specific output, measure how much prediction changes when specific features are altered)
                          ex) SHAP(use Game Theory for importance score), KernelSHAP, use Local Gradients to test feature sensitivity
    3.Visualization - create Visual Representations to easily see how model makes choices
                      ex) use decision-tree algorithms and computer vision, Grad-CAM(generate heatmap over an img on influence in classification), XGBoost(Built-in visualization tools for complex trees)
 Explainability
  - Ante-hoc & Post-hoc
  - Towards AI that are General / Supervised / Unsupervised / RL / Computer vision img detection / Generative

3) Comparison axes
  - Axis 1: Interpretability(white-box) : understand "how" of generation via internal model structures directly, interpretability <-> accuracy tradeoff
            .vs.
            Explainability(black-box) : convey ML behavior in human-understandable terms with no need of internal knowledge

  - Axis 2: Ante-hoc(methods of transparency being built in model's design, Before)
            .vs.
            Post-hoc(methods of applying after the model is trained, After)
  
  - Axis 3: Local Fidelity(focus on specific individual predictions)
            .vs.
            Global Fidelity(assess overall behavior across an entire dataset)

============================================================
B. BRANCH-BY-BRANCH
===

--------------------------------------------------------------------------------
General - Branch 1: LIME (Local Interpretable Model-agnostic Explanations)
 - provides local, post-hoc explanations for black-box models by perturbing input data and fitting a simpler, interpretable linear surrogate model to the outputs
 - primary objective is to identify the most influential features for specific individual predictions

--------------------------------------------------------------------------------
General - Branch 2: Shapley Values / SHAP
 - derived from cooperative game theory and assigns a unique importance value to each input feature based on its contribution to a specific model output
 - provides a theoretically grounded way to quantify and rank feature importance for individual instances

--------------------------------------------------------------------------------
General - Branch 3: Partial Dependence Plots (PDP)
 - quantify the marginal effect of one or two features on the predicted outcome of a model while accounting for the average effect of all other features
 - particularly valuable for visualizing global relationships and identifying potential biases in datasets

--------------------------------------------------------------------------------
General - Branch 4: Individual Conditional Expectation (ICE) Plots
 - visualize the relationship between a feature and the prediction for individual instances, helping to uncover heterogeneous relationships that average plots might miss
 - allow for the identification of specific feature interactions at different levels for different instances

--------------------------------------------------------------------------------
General - Branch 5: Counterfactual Explanations (CE)
 - provides causal explanations by identifying the minimal changes required in the input features to lead to a different, desired model outcome
 - helps users understand "what if" scenarios and provides actionable insights for changing outcomes

--------------------------------------------------------------------------------
General - Branch 6: Anchors
 - identify high-precision "if-then" decision rules that reliably explain model predictions in a local region
 - ensure the explanation holds with high confidence across a large proportion of similar cases

--------------------------------------------------------------------------------
General - Branch 7: Model Distillation
 - transfers knowledge from a large, complex "teacher" model to a smaller, more interpretable "student" model while preserving performance
 - used to maintain accuracy while reducing computational costs and increasing transparency

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
Supervised - Branch 1: Hybrid xAI Approaches
 - integrate multiple explanation strategies, such as LIME with SHAP, to provide a more complete understanding of model behavior
 - designed to address the limitations of individual techniques by combining local and global perspectives

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
Unsupervised - Branch 1: t-SNE (t-Distributed Stochastic Neighbor Embedding)
 - dimensionality reduction technique used to visualize high-dimensional data in 2D or 3D spaces
 - helps domain experts explore and understand learned data structures by preserving local patterns in the dataset

--------------------------------------------------------------------------------
Unsupervised - Branch 2: Explainable Clustering Methods
 - human-readable descriptions, feature importance rankings, or rules to explain why data points were grouped together into specific clusters
 - provide transparency into the clustering process, which is often used for customer segmentation or anomaly detection

--------------------------------------------------------------------------------
Unsupervised - Branch 3: Bayesian Rule Lists
 - combines decision trees and ordered if-then rules using probabilistic modeling to capture interpretable patterns in unsupervised datasets
 - highly transparent and allows for the quantification of uncertainty in model outcomes

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
RL - Branch 1: Attention-based Mechanisms
 - acts as a weighting function that allows an agent to focus on vital components of the environment while filtering out less critical information
 - provides a clearer understanding of how agents prioritize different aspects of their surroundings

--------------------------------------------------------------------------------
RL - Branch 2: Saliency Mapping
 - identifies and highlights the specific regions in the input space that are most influential in an agent's decision-making process
 - generates heatmaps that allow stakeholders to track and validate the agent's reasoning in a more intuitive manner

--------------------------------------------------------------------------------
RL - Branch 3: Causal XRL Framework (CXF)
 - integrates reinforcement learning with external ontologies and causal reasoning to allow agents to justify their decisions through cause-and-effect relationships
 - human-readable justifications that increase trust and accountability in high-stakes domains

--------------------------------------------------------------------------------
RL - Branch 4: Local-Linear Models
 - approximates an agent's learned policy with simpler, locally linear models in specific regions of the input space
 - provides a transparent understanding of the decision-making process by showing how input features interact with predictions locally

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
Computer vision img detection - Branch 1: Guided Backpropagation
 - post-hoc technique for CNNs that backpropagates through activation functions to identify and visualize image features that maximized neuron activation
 - helps interpret activity in both convolutional and fully connected layers of the model

--------------------------------------------------------------------------------
Computer vision img detection - Branch 2: Grad-CAM (Gradient-weighted Class Activation Mapping)
 - overlays a heatmap on original images to showcase the specific regions the model deemed important for a classification decision
 - used in medical imaging to provide visual explanations for diagnoses or anomalies

--------------------------------------------------------------------------------
Computer vision img detection - Branch 3: Deep SHAP
 - combines Shapley values with backpropagation to decompose output predictions by quantifying the contribution of every individual pixel
 - a non-biased assessment of feature attribution by analyzing each pixel or voxel independently

--------------------------------------------------------------------------------
Computer vision img detection - Branch 4: Testing with Concept Activation Vectors (TCAV)
 - high-level, human-defined concepts (like "wheels" or "stripes") to measure how sensitive a model's prediction is to those concepts rather than raw pixels
 - a quantifiable mapping of feature importance using pre-defined human knowledge

--------------------------------------------------------------------------------

--------------------------------------------------------------------------------
Generative - Branch 1: Layer-wise Relevance Propagation (LRP)
 - attributes relevance scores to neurons by decomposing an output prediction into contributions from input features
 - used to visualize which pixels significantly influence the generation or segmentation of synthetic content

--------------------------------------------------------------------------------
Generative - Branch 2: InfoGAN
 - maximizes mutual information between latent codes and the generated output to encourage the model to capture explainable semantic features
 - help researchers understand the internal generative mechanisms by making latent representations more interpretable

--------------------------------------------------------------------------------
Generative - Branch 3: Disentangled Representation GAN (DR-GAN)
 - designed to learn entirely disentangled and explainable representations using specific regularization terms
 - allows users to manipulate and explain specific aspects of the generated samples independently

--------------------------------------------------------------------------------
Generative - Branch 4: GAN Dissection
 - identifies and visualizes the specific neurons responsible for generating distinct objects (like doors or trees) within a GAN
 - allows researchers to manipulate or remove these features to analyze the role of individual neurons in the output

--------------------------------------------------------------------------------
Generative - Branch 5: DragGAN
 - interactive method that allows users to "drag" points in GAN-generated images to control attributes such as pose, shape, and layout
 - uses feature-based motion supervision and point tracking to provide precise control and interpretability over the generative manifold
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------

============================================================
C. GAPS & IDEAS _ while or after finishing
===
1) Prefered Branches : have more questions or ideas, related to interest fields
2) Gaps : underexplored or underexplained fields, seemingly dangerous assumptions
3) Possible ideas / research questions
============================================================