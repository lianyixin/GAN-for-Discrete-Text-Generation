# GAN-for-Sequence-Generation

## Why sequence generation
Dialog systems, machine translation, image captioning, etc. 

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

LeakGAN: 
During adversarial training process, the discriminator reveals its internal state to guide the generator more informatively and frequently. (Generator -> Manager + Worker lstm network, get features from discriminator)

![leakgan](https://pbs.twimg.com/media/DRPIgb4XkAADSkV.jpg)

## Objective-Reinforced
### Fixed objective reward component
### Multi-feature output reward
SentiGAN:

LabelGAN:

### StyleGan
