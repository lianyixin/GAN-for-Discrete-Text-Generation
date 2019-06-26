# GAN-for-Sequence-Generation

## Why sequence generation
Dialog systems, machine translation, image captioning, data augmentation, etc. 

## The way for sequence generation
### Conventional
### MLE
Drawbacks: exposure bias and label bias; general, boring, repeat.
### Naive RL
Drawbacks: biased and correlate poorly with human judgments. less of semeantic properties.
### GAN
An approach for estimating intractable probabilities.
### VAE
Without the problem of generating discrete data, however, it has more constraints and restrictions than GAN.

## SeqGAN, an impactful way for discrete sequence generation
Generally, GAN is applied for continuous problem like image generation. For discrete sequence generation, the gradient of loss from discriminator cannot transferred to the generator. SeqGAN innovatively incorporated RL into the update of generator gradient using Monte Carlo policy gradient estimation. 

![seqgan](https://cdn-images-1.medium.com/max/1200/0*FUwClIx3rko7vbFG)

However, after several experiments, it shows the generated texts face the problem of poor quality. 
  * The entire text lacks intermediate information about text structure - The binary guiding signal from D is sparse as it is only available when the whole text sample is generated. 
  * Another problem is mode collapse - GAN prefers to generate samples around only a few modes while igoring other modes, lack of diversity. 
  * If the discriminator is too perfect, it's hard for generator to learn - gradient vanishing. 

## Improvement 
### Loss Function
WGAN:

RankGAN:

### Generator Gradient Equation
### Different RL methods
### Reward Design
 * Rescale reward for solving vanishing gradients
 * Change classifer_based discriminator to Language model and redesign the reward to be the sentence-level reward + word-level reward.
### Network Architecture
DPGAN:

![dpgan](https://cdn-images-1.medium.com/max/1600/1*8G0FmWqfWDJXCIUbrY-JUA.png)

LeakGAN: 
During adversarial training process, the discriminator reveals its internal state to guide the generator more informatively and frequently. (Generator -> Manager + Worker lstm network, get features from discriminator)

![leakgan](https://pbs.twimg.com/media/DRPIgb4XkAADSkV.jpg)

Architecture from Dr.Li:
Share the information from Discriminator with Generator (same as LeakGAN, but different design)

## Objective-Reinforced
Problem Define: Generate target sentence in specific domain with 2 datasets, one large general domain dataset A, and one specific domain dataset B.

### Fixed objective reward component
### Multi-feature output reward
SentiGAN:

LabelGAN:

### Style transfer
Most articles explore transferring the text from the source style to the target style. Most existing unsupervised approaches share a core idea of disentangling content and style of texts. 

VAEs are commonly used to learn the hidden representation of inputs for dimensionality reduction, and have been found to be useful for representing the content of the source. Cycle consistency proposes to reconstruct the input sentence from the content representation, by forcing the model to keep the information of the source sentence. 

![crossalignment](http://isukorea.com/media/PNG/latent.PNG)

![rl_based_style_transfer](https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/8f0bf19b5c76f26dffbcf8dfd03c6a7a8b58d716/4-Figure2-1.png)


