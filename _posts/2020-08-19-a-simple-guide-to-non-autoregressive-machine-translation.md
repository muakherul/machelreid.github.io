---
layout: single 
author: Machel Reid
toc: true

---

### Introduction
Generally, when we think about generation in NLP, we think of it as going from left-to-right (or right-to-left) -- i.e. you generate one token at a time. For example, take this diagram of this language model below:

[diagram]

You can see that the prediction of the word *word* is conditioned on the previous prediciton of the word *another word*. This form of generation is commonly referred to as **autoregressive generation** - each output is conditioned on the previous one and a sequence is generated sequentially.

However, what if you could generate all the tokens in your sequence *at-once*. Recently, with the introduction of the Transformer -- in which sequence-level operations can be computed in parallel -- **non-autoregressive** translation ... .

In this post, I aim to provide a brief overview of exisiting non-autoregressive translation models and summarize some of the recent advances in this domain.

### Autoregressive generation
Overview of LMs

## Non autoregressive

### Non-autoregressive Translation (Jiatao's paper)

### Latent Variable Non-autoregressive Translation - Raphael's paper

### CMLMs (and the endless derivatives) - Marjan's paper 

### LevT - Jiatao's paper

### 
