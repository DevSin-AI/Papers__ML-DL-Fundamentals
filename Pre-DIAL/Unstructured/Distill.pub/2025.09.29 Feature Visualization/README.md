2025.09.29

# Feature Visualization : How neural networks build up their understanding of images.

Link : https://distill.pub/2017/feature-visualization/

-----
1.Optimization
Starting from random noise, iteratively tweak the input img for targets.

- Target (n:layer index, x&y: spatial position, z:channel index, k:class index)
  For Individual features -> highest value target
      Neuron( layer n[x,y,z])
      Channel(layer n[:,:,z])
  For understanding a layer -> DeepDream objective for interesting images
      Layer(layer n[:.:.:]^2)
  For examples of output classes -> highest value on either pre or post softmax
      Class Logits(pre_softmax[k])
      Class Probability(softmax[k])

  ...etc

        ### What is _Deep Dream Objective_ ###
        #  Objective used for layers - trying to amplify patterns that the layer already detects.
        #  Starting with a real img not noise, it does a graident ascent on the squared activations of the layer.
        #  The img developas hallucinatory, fractal-like patterns as features get exaggerated repeatedly.
        ######################################

Optimization has the advantage of
    Provides powerful way of understanding what the model is looking for by separating the causing behavior
    Flexibility : can easily extend our targets, visualizing for unique groups of targets, etc.

-----
2.Diversity
- When examples by optimization are created, it is an important point to consider if the examples show the full picture. And for this, we can look across the whole spectrum of activations.
      Positive optimized/ Maximum activation examples/ Slightly positive activation examples
      Negative optimized / Minimum activation examples/ Slightly negative activation examples

- Models may respond to a wide range of inputs. A classifier trained for a target should recognize all variations.
  (Dog = close up face of dogs, full picture of dogs on the side or back, etc)

1.Approach from Understanding Intra-Class Knowledge Inside CNN( Donglai Wei, et al.)
  * reminder to read the paper from arXiv. (https://arxiv.org/pdf/1507.02379)*
Attempts to demonstrate this "intra-class" diversity by recording activations over the entire training set, clustering them and analyzing the cluster centroids. Each cluster represents a different style or variation, helping to understand how the network organizes features hierarchically.

2.Approach from Multifaceted Feature Visualization: Uncovering the Different Types of Features
Learned By Each Neuron in Deep Neural Networks( Anh Nguyen, et al. )
  * reminder to read the paper from arXiv. (https://arxiv.org/pdf/1602.03616)*
Search dataset for diverse examples and use those as starting points of optimization, so different pictures lead the optimization to different features.
Had limited success.

      2-1.Approach from Plug & Play Generative Networks: Conditional Iterative Generation of Images in Latent Space ( Anh Nguyen, et al. )
       * reminder to read the paper from arXiv. (https://arxiv.org/pdf/1602.00005)*
      Evolving the method of 2, it replaces the diverse seeds to come from a generative model rather than from the fixed dataset examples. Exploring a broader and more controlled diversity of starting points, it worked better than 2.

3.Approach/Suggestion from the aritcle.
Adding a diversity term to one's objective that pushes multiple examples to be different from each other. Basically enforcing diversity in the objective itself.
The aritcle shows little understanding of its benefits suggesting possibilities to penalize the cosine similarity or use ideas from style transfer(3-1.)
Diversity terms work by explicitly pushing feature space representations apart.

      3-1.Approach from A neural algorithm of artistic style( L.A. Gatys, et al. )
       * reminder to read the paper from arXiv. (https://arxiv.org/pdf/1508.06576)*
      The article borrows this paper's idea and uses the following;
      -Gram matrix G : G(i,j) is the dot product between the response of layer i and layer j.
      -Diversity term C = the negative pairwise cosign similarity of pairs of visualizations.
$$
C_{\text{diversity}} = - \sum_a \sum_{b \neq a} 
\frac{ \text{vec}(G_a) \cdot \text{vec}(G_b) }
     { \| \text{vec}(G_a) \| \, \| \text{vec}(G_b) \| }
$$

Shortcomings of Diversity-term approach
 - Pressures of different examples can cause unrelated artifacts to appear
 - Pressures may make examples be different in unnatural ways. ((ex) unable to seperate obvious items from each other.)
 - Neuron ambiguity; some neurons represent mixtures of unrelated concepts - this is a fundamental issue that shows that neurons aren't the right semantic units for understanding neural nets.

-----
3.Combinations of neurons
Combinations of neurons are what really works to represent images in neural networks.

If an activiation space is defined as all possible combinations of neuron activations,
individual neuron activations can be seen as basis vectors of this space
leading to a meaningful group of neuron activations to be seen as a vector.

Intriguing properties of neural networks(C. Szegedy, et al.) notes that random directions seem just as meaningful as the directions of basis vectors.
Network Dissection: Quantifying Interpretability of Deep Visual Representations( D. Bau, et al.) notes that the directions of basis vectors to be interpretable more often than random directions.
The article states that random directions often seem interpretable but at a lower rate than basis directions.

We can also define interesting directions in activation space by doing arithmetic on neurons.
(ex. black and white neuron + mosaic neuron creates a black and white mosaic)

The article states that it doesn't know how to select meaningful directions, and how directions interact.
As this article is a few years old, newer papers should be read instead.
 *Note to self on what to read for this*
      - The Local Interaction Basis: Identifying Computationally-Relevant and Sparsely Interacting Features in Neural Networks
      https://arxiv.org/pdf/2405.10928
      - Identifying Interpretable Visual Features in Artificial and Biological Neural Systems
      https://arxiv.org/pdf/2310.11431
      - Modularity in Transformers: Investigating Neuron Separability & Specialization
      https://arxiv.org/pdf/2408.17324
      - Discovering Influential Neuron Path in Vision Transformers
      https://www.arxiv.org/pdf/2503.09046

-----
4.Challenges and Limitations
Just optimizing an image to make neurons isn't really that straight forward as noise and meaningless high-frequency patterns that the network responds strongly to will overtake the result.
This happens in case of no regulation, like a high learning rate.
      'Intriguing properties of neural networks'(Szegedy, et al.) is brought up as adversarial examples. 

The article states that the reason of these unwanted patterns forming is unknown, only telling that the important part seems to be that the strided convolutions and pooling operations create high frequency patterns in the gradient.

Three main families of regularization options are used to avoid this.

A) Frequency penalization : Directly targets the high frequency noise
      - May explicitly penalize variance between neighboring pixels
        or implicitly penalize high-frequency noise by blurring the image each step
      - Has limit of also discouraging legitimate high-frequency features,
        that can be slightly improved by a bilateral filter which preserves edges intead of blurring.

B) Transformation robustness : Tries finding examples that activate even with transformation
      - Jitter, rotate or scale the image before applying optimization steps, see if it's still activating highly.
      - Even small amounts seem very effective,
        especially combined with a more general regularizer for high-frequencies

C) Learned priors : Optimize from inside the latent space of a generative model trained on real data
      - Results are the most realistic,
        but it may be unclear what came from the model being visualized and what is from the prior
      - Approaches
       1. Learn a generator that maps points in a latent space to examples of data and optimize within.
       2. Learn a prior that gives access to the gradient of probability.
          Jointly optimize for the prior along the objective

-----
5.Preconditioning and Parameterization
Transformation robustness - reduces high frequencies in the gradient rather than the visualization itself
->
Preconditioning == transforming the gradient
 Optimizing for the objective in another parameterization of the space or under a different notion of distance.
 By transformation, the direction and how fast the optimization gets changes but not the minimum.
 Therefore, the right preconditioner can make optimization radically easier.

 Gradient descent is sensitive to scale and correlation, so Decorrelation and Whitening(정규화) is good for a good preconditioning.
 Do gradient descent in the  Fourier basis with frequencies scaled
 It allows all directions to be handled equally, making gradient descent faster and more stable.
      Directions : L2(basically an outline of target) / L∞ (for advisary, high frequency is hightened) / Decorrelated(L2 decorrelated. Better results and lesser high-freq)
 
 The article questions if the preconditioner is just adding speed to the gradient descent or if it has regularization properties.
  - Gradient decent seem to continue imporving as steps increase - slow growth but not converged
  - Even with no other regularizers, the preconditioner seems to reduce high-frequency patterns.
 While in convex problems preconditioners are formally analyzed most as accelerators,
 in non-convex,deep learning; they act like implicit regularizers - doing both.

