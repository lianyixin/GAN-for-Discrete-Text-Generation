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

![gan](https://cdn-images-1.medium.com/max/1600/1*M_YipQF_oC6owsU1VVrfhg.jpeg)

### 5. VAE
Without the problem of generating discrete data, however, it has more constraints and restrictions than GAN.

## [SeqGAN](https://arxiv.org/abs/1609.05473), an impactful way for discrete sequence generation
Generally, GAN is applied for continuous problem like image generation. For discrete sequence generation, the gradient of loss from discriminator cannot transferred to the generator. SeqGAN innovatively incorporated RL into the update of generator gradient using Monte Carlo policy gradient estimation. 

 * RNN-based Generator + Classifier-based Discrminator
 * Use MLE to pretrain G and D
 * Monte Carlo for reward, policy gradient for updating G - effectively estimate the reward for an unfinished sentence. 

![seqgan](https://cdn-images-1.medium.com/max/1200/0*FUwClIx3rko7vbFG)

![seqgan_equation](https://cdn-images-1.medium.com/max/1600/0*JcHrudkUiINkgXhG.png)

However, after several experiments, it shows the generated texts face the problem of poor quality. 
  
  * Mode collapse - GAN prefers to generate samples around only a few modes while igoring other modes, lack of diversity. 
  
  * Gradient vanishing - If the discriminator is too perfect, it's hard for generator to learn.
  
  ![NLL_score](https://www.researchgate.net/publication/308324937/figure/fig1/AS:408264924778496@1474349351242/Negative-log-likelihood-performance-with-different-pre-training-epochs-before-the.png)

  * CNN Discriminator not good enough - Lack of position information, max pooling focuses on the highest scores.

  * Sparse Reward
  
## Research Direction
 * Loss Function
 * RL Methods 
 * Reward Design
 * Network Architecture
 * Domain-Reinforced

### 1. Loss Function
[WGAN](https://arxiv.org/abs/1701.07875):

In order to solve gradient vanishing problem. Introduce the w distance into GAN. Remove the last sigmoid layer of Discriminator.

![wgan_equation](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/wgan.png)

![wgan](https://cdn-images-1.medium.com/max/1600/1*-VajV2qCbPWDCdNGbQfCng.png)

### 2. RL methods
MCST comes at significant computational cost.

### 3. Reward Design
[RankGAN](https://arxiv.org/abs/1705.11001):

Rather than training the discriminator to learn and assign absolute binary predicate for individual data sample, RankGAN is able to rank a collection of human-written and machine-written sentences by giving a reference group. 

![rankgan_equation](https://tobiaslee.top/img/rank_gan.png)

![rankgan](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/rankgan.png)

[DPGAN](https://arxiv.org/abs/1802.01345):

Change classifer_based discriminator to Language model and redesign the reward to be the sentence-level reward + word-level reward.

![dpgan](https://cdn-images-1.medium.com/max/1600/1*8G0FmWqfWDJXCIUbrY-JUA.png)

![dpgan_graph](https://tobiaslee.top/img/dp-gan.png)

### 4. Network Architecture
[LeakGAN](https://arxiv.org/abs/1709.08624): 

During adversarial training process, the discriminator reveals its internal state to guide the generator more informatively and frequently. (Generator -> Manager + Worker lstm network, get features from discriminator)

![leakgan](https://pbs.twimg.com/media/DRPIgb4XkAADSkV.jpg)

### 5. Domain-Reinforced
Problem Definition: 

Generate target sentence in specific domain with 2 datasets, one large general domain dataset A, and another dataset B for the specific domain.

### 5.1 Additive reward

[ORGAN](https://arxiv.org/abs/1705.10843):

![organ](https://www.groundai.com/media/arxiv_projects/91267/figs/ORGAN_schema.png)

### 5.2 Multiclass output reward

[SentiGAN](https://www.ijcai.org/proceedings/2018/0618.pdf):

![sentigan](https://www.researchgate.net/profile/Ke_Wang185/publication/326202527/figure/fig1/AS:654921988853768@1533156978666/The-framework-of-SentiGAN-with-k-generators-and-one-multi-class-discriminator.png)

### 5.3 Style transfer

Most articles explore transferring the text from the source style to the target style. Most existing unsupervised approaches share a core idea of disentangling content and style of texts. 

VAEs are commonly used to learn the hidden representation of inputs for dimensionality reduction, and have been found to be useful for representing the content of the source. Cycle consistency proposes to reconstruct the input sentence from the content representation, by forcing the model to keep the information of the source sentence. 

[Style Transfer from Non-Parallel Text by Cross-Alignment](https://arxiv.org/abs/1705.09655)

![crossalignment](http://isukorea.com/media/PNG/latent.PNG)

Another way is by the use of a style classifier without explicitly separating content and style. 

[Reinforcement Learning Based Text Style Transfer without Parallel Training Corpus](https://arxiv.org/abs/1903.10671)

![rl_based_style_transfer](https://github.com/lianyixin/GAN-for-Sequence-Generation/blob/master/rlbasedstyletransfer.png)

[CGAN](https://arxiv.org/abs/1411.1784):

Feeding the data y which is conditioned on to both generator and discriminator.

![cgan](https://golden-storage-production.s3.amazonaws.com/topic_images/23a36a66d85947c7a0fe4a2ced52914e.png)

[StyleGAN](https://arxiv.org/abs/1812.04948) for image style transfer:

![stylegan](https://cdn-images-1.medium.com/max/1600/0*uqn4slMHrFYkFmjS.png)
