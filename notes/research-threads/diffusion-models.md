---
date: 01/03/23
---

# Diffusion models 


## Introduction 

[Diffusion](https://arxiv.org/abs/1503.03585) models (DM's for short) have taken the world by storm in the year of 2022--from Dalle 2 to Stable Diffusion. It started with unconditional image generation (generate an image after training on an IID image distribution) via [DDPM](https://arxiv.org/abs/2006.11239)'s as a step up from the unstable GAN's. [Dalle 2](https://openai.com/dall-e-2/) connected large language modeling (via [CLIP](https://openai.com/blog/clip/)) and diffusion models (as compared to [VQGAN](https://arxiv.org/pdf/2012.09841.pdf) in Dalle 1). [Stable diffusion](https://github.com/CompVis/stable-diffusion) made this open source and more "stable" by using [latent diffusion models](https://openaccess.thecvf.com/content/CVPR2022/papers/Rombach_High-Resolution_Image_Synthesis_With_Latent_Diffusion_Models_CVPR_2022_paper.pdf) where latent representations (from a pre-trained autoencoder) of images were connected to text. 

Importantly, the above paragraph talks about the DDPM probablistic model framework to diffusion models, which in turn, have deep connections to variational autoencoders. There exists other generative paradigms such as:

- score-based generative modeling 
- stochastic differential equations 

Song's work ([thesis](https://stacks.stanford.edu/file/druid:zy983tp3399/submit-augmented.pdf)) provides a good overview of the above. See Song's [blog post](https://yang-song.net/blog/2021/score/) for an overview. In addition of course, are the old paradigms of generative learning: 

- GAN's 
- VAE's 




## Connecting text to image 

The main source of hype around diffusion models came when users could generate impressive, realistic images given any description they could imagine. 

