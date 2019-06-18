# GAN-for-Sequence-Generation
My personal learning for sequence generation using GAN

## Why sequence generation
Q&A, 

## The way for sequence generation
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

However, after several experiments, it shows the generated texts face the problem of poor quality. Another problem is mode collapse - GAN prefers to generate samples around only a few modes while igoring other modes, lack of diversity.  

## Improvement 
### Loss Function
### Generator Gradient Equation
### Different RL methods
### Reward Design
### Network Architecture

## Objective-Reinforced
### Fixed objective reward component
### Multi-feature output reward
SentiGAN:

LabelGAN:

### StyleGan
