---
title: Generative Adversarial Networks
subtitle: Generative Adversarial Networks or in short GAN's have the most
  interesting and appealing applications in my opinion ranging from generating
  new samples for data augmentation to create deepfakes or transforming images
  from one domain to the other domain. So, I thought of writing about this and
  appreciate the math behind it.
date: 2022-07-02T14:06:24.202Z
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
This blog requires the basic understanding of Probability and Statistics and Neural Nets. 

# Problem Statement

Suppose, we are given the samples from a distribution and distribution is unknown to us. These samples could be anything from images to audio. Our aim is to generate more samples that looks like they came from the same distribution. In order to do so, we try to model a distribution that approximates the target distribution.

# Basics

Adversarial refers to conflict/opposition. So, GANs consists of 'adversarial' training between two parties (in our case, the parties would be neural nets) such that we will be able to 'generate' new samples from the data. Those parties are Generator and Discriminator. 

The work of the Generator is to transform a easy to sample distribution (like a D-dimensional Normal Distribution etc.) to a probability distribution that we want as close as the target distribution. Discriminator is a Binary Classifier which gives the probability whether the sample came from the data. So, both these parties conflict with each other in such a way so that the Generator tries to generate more realistic samples by the feedback that Discriminator gives on the samples. 

So, this is some kind of Police-Scammer case, where Scammer (Generator) tries to generate fake currency and Police (Discriminator) distinguishes fake and real currency and we want Scammer to generate realistic currency such that the Police gets confused between the real and fake. So, we can see some kind of adversary.  

Why do we want both these parties to get trained? It's because we neither want the tough Discriminator which won't help Generator to progress nor a poor Discriminator by which Generator won't produce realistic samples. 

## Notations

Say the data is denoted as $x$. The data underlies under the distribution $p_d$. Let the easy to sample distribution be denoted as $p_z$, distribution transformed be denoted as $p_g$ and the parameters of Generator $G$ and Discriminator $D$ denoted by $\theta_g$ and $\theta_d$ respectively. The loss function is denoted as $\mathcal{L}$.

# Loss function

Let's use BCE (Binary Cross-Entropy) loss in this case. 

{{< math >}}
$$
\mathcal{L}(\theta*g,\theta*d)  = \mathbb{E}_{x \sim p_d(x)}[-log(D(x))]+\mathbb{E}_{x \sim p_g(x)}[-log(1-D(x))] 
$$
{{< /math >}}
{{< math >}} 
$$
  = \mathbb{E}_{x \sim p_d(x)}[-log(D(x))]+\mathbb{E}_{z \sim p_Z(z)}[-log(1-D(G(z)))]
$$
{{< /math >}}

The Generator $G$ and Discriminator $D$ play the two-player mini-max game with the loss function $\mathcal{L}$. Generator wants $D(G(z))$ to be close to 1 while Discriminator $D$ wants it to close to 0 and $D(x)$ close to 1. So, $G$ wants to maximise the $\mathcal{L}$ while $D$ wants to minimise $\mathcal{L}$.

{{< math >}}
$$ 
    \max_{G} \min_{D} \mathcal{L}(\theta_g,\theta_d)
$$
{{< /math >}}

Analysis

Let's see why this works. First, let's check what is the optimal discriminator for us. Fix the Generator $G$. 
{{<math>}}
$$ 
  \mathcal{L}(\theta_g,\theta_d) = \mathbb{E}_{x \sim p_d(x)}[-log(D(x))]+\mathbb{E}_{x \sim p_g(x)}[-log(1-D(x))]
$$
{{</math>}}
{{<math>}}
$$ 
  = \int_x p_d(x)(-log(D(x))) + p_g(x)(-log(1-D(x))) dx 
$$
{{</math>}}
Now, differentiating this integral with respect to $D(x)$ and equating with zero gives the optimal Discriminator $D^\ast(x)$. (Exercise for the reader). Assume the paramters of $D^\ast(x)$ be $\theta^\ast_d$.
{{<math>}}
$$ 
  D^\ast(x) = \frac{p_d(x)}{p_d(x)+p_g(x)}
$$
{{</math>}}
Now, let's look at the Generator part. 
{{<math>}}
$$ 
  \mathcal{L}(\theta_g,\theta^\ast_d) = \mathbb{E}_{x \sim p_d(x)}[-log(D^\ast(x))]+\mathbb{E}_{x \sim p*g(x)}[-log(1-D^\ast(x))]
$$
{{</math>}}
{{<math>}}
$$ 
  = \mathbb{E}_{x \sim p_d(x)}[-log(p_d(x))+log(p_d(x)+p_g(x))] 
$$
{{</math>}}
{{<math>}}
$$ 

* \mathbb{E}_{x \sim p_g(x)}[-log(p_g(x))+log(p_d(x)+p_g(x))]
  $$
  {{</math>}}
  {{<math>}}
  $$ 
    = 2log(2) - D_{KL}(p_d||\frac{p_d+p_g}{2}) - D_{KL}(p_g||\frac{p_d+p_g}{2})
  $$
  {{<\math>}}
  {{<math>}}
  $$
    = 2log(2) - 2JSD(p_d||p_g)
  $$
  {{</math>}}
  where $D_{KL}$ and $JSD$ are KL Divergence and Jenson Shannon Divergence respectively. So, $JSD$ is a non-negative quantity and attains zero when both the distributions are equal. Since, the Generator $G$ wants to maximise the loss function hence the global optimum will attain when $p_g = p_d$ and that's what we wanted.


The drawback of GANs is sometimes the Generator is able to generate only handful of samples and not able to produce variety of samples. This from of failure is known as Mode Collapse.