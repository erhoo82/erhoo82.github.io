---
title: "[paper review][system] ZeRO: Memory Optimizations Toward Training Trillion Parameter Models"
layout: post
date: 2021-10-30
headerImage: false
tag:
- Deep learning 
- Memory usage optimization
category: blog
author: Sangkug Lym
description: Paper review: ZeRO
hidden: true
---

## Problems

- Training a language model with billions of parameters needs a huge GPU memory space. Unlike the known memory requirement to allocate (1) model parameters and (2) input activations (needed to compute the derivate loss in backprop), training involves extra memory for (3) optimizer states, (4) gradients, (5) master parameters (half-precision training), and (6) temporal buffers. Due to the high memory requirement, training a large model often needs a large training system with hundreds of GPU nodes and the model is deployed using MP (model-parallelism). However, due to 
- 

---

## Contributions

- xxxx
- xxxx

---

## Main ideas

- xxxx
- xxxx

---

## Key results

- xxxx
- xxxx

---

## My thoughts and potential follow-ups

- xxxx
- xxxx
