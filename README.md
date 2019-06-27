# GAN-for-Sequence-Generation

## Why sequence generation
Dialog systems, machine translation, image captioning, data augmentation, etc. 

## The way for sequence generation
### 1. Conventional
Plan-Based, Class-Based, Phrase-Based, Corpus-Based, etc.
### 2. MLE
Drawbacks: exposure bias and label bias; general, boring, repeat.
### 3. Naive RL
Drawbacks: biased and correlate poorly with human judgments. Lack of semeantic properties.
### 4. GAN
An approach for estimating intractable probabilities.

![gan](https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2017/06/11000153/g1.jpg)

### 5. VAE
Without the problem of generating discrete data, however, it has more constraints and restrictions than GAN.

## SeqGAN, an impactful way for discrete sequence generation
Generally, GAN is applied for continuous problem like image generation. For discrete sequence generation, the gradient of loss from discriminator cannot transferred to the generator. SeqGAN innovatively incorporated RL into the update of generator gradient using Monte Carlo policy gradient estimation. 

 * RNN-based Generator + Classifier-based Discrminator
 * Use MLE to pretrain G and D
 * Monte Carlo for reward, policy gradient for updating G

![seqgan](https://cdn-images-1.medium.com/max/1200/0*FUwClIx3rko7vbFG)

![seqgan_equation](https://cdn-images-1.medium.com/max/1600/0*JcHrudkUiINkgXhG.png)

![another_equation]()

However, after several experiments, it shows the generated texts face the problem of poor quality. 
  * The entire text lacks intermediate information about text structure - The binary guiding signal from D is sparse as it is only available when the whole text sample is generated. 
  
  ![lack_intermediate_information]()
  
  * Mode collapse - GAN prefers to generate samples around only a few modes while igoring other modes, lack of diversity. 
  
  ![mode_collapse]()
  
  * Gradient vanishing - If the discriminator is too perfect, it's hard for generator to learn.
  
  ![gradient_vanishing]()

## Improvement Direction
 * Loss Function
 * RL Methods 
 * Reward Design
 * Network Architecture
 * 
 
### 1. Loss Function
WGAN:

In order to solve gradient vanishing problem. Introduce the w distance into GAN. Remove the last sigmoid layer of Discriminator.

![wgan_equation](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/wgan.png)

![wgan](https://cdn-images-1.medium.com/max/1600/1*-VajV2qCbPWDCdNGbQfCng.png)

### 2. RL methods
MCST comes at significant computational cost.

### 3. Reward Design
RankGAN:

Rather than training the discriminator to learn and assign absolute binary predicate for individual data sample, RankGAN is able to rank a collection of human-written and machine-written sentences by giving a reference group. 

![rankgan_equation](https://tobiaslee.top/img/rank_gan.png)

![rankgan](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/rankgan.png)

DPGAN:

Change classifer_based discriminator to Language model and redesign the reward to be the sentence-level reward + word-level reward.

![dpgan](https://cdn-images-1.medium.com/max/1600/1*8G0FmWqfWDJXCIUbrY-JUA.png)

### 4. Network Architecture
LeakGAN: 

During adversarial training process, the discriminator reveals its internal state to guide the generator more informatively and frequently. (Generator -> Manager + Worker lstm network, get features from discriminator)

![leakgan](https://pbs.twimg.com/media/DRPIgb4XkAADSkV.jpg)

### 5. Objective-Reinforced
Problem Define: 

Generate target sentence in specific domain with 2 datasets, one large general domain dataset A, and one specific domain dataset B.

### Fixed objective reward component

### Multi-feature output reward
SentiGAN:

LabelGAN:

### Style transfer
Most articles explore transferring the text from the source style to the target style. Most existing unsupervised approaches share a core idea of disentangling content and style of texts. 

VAEs are commonly used to learn the hidden representation of inputs for dimensionality reduction, and have been found to be useful for representing the content of the source. Cycle consistency proposes to reconstruct the input sentence from the content representation, by forcing the model to keep the information of the source sentence. 

![crossalignment](http://isukorea.com/media/PNG/latent.PNG)

Another way is by the use of a style classifier without explicitly separating content and style. 

![rl_based_style_transfer](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/rlbasedstyletransfer.png)

CGAN:

Feeding the data y which is conditioned on to both generator and discriminator.

![cgan]()

StyleGAN for image style transfer:

![stylegan](https://cdn-images-1.medium.com/max/1600/0*uqn4slMHrFYkFmjS.png)

Inspiration for our problem:

