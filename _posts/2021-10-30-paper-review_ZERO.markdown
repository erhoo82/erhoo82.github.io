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

My thoughts...

## Problem summary with the addition of my thoughts

__High memory requirement:__ Training a language model with billions of parameters needs a huge GPU memory space. Unlike the well-known memory requirement of training such as the allocation of (1) model parameters and (2) input activations (needed to compute the derivate loss in backprop), training involves extra memory needs: (3) optimizer states, (4) gradients, (5) master parameters (half-precision training), (6) temporal buffers (to hold inputs or outputs upon eGPU operator execution), and (7) input buffers. Especially, optimizer states becomes the biggest memory occupier when training a large language model. Due to the high memory requirement, a large training system with hundreds of GPU nodes is needed and this often limits the size of model to train.

__Suboptimal parallelism:__ DP (Data Parallelism) is the most commonly used technique to scale a training system. However, DP duplicates model parameters, optimizer states, and parameter gradients thus making it difficult to use in training a large language model. Instead, MP (Model Parallelism) divides the model parameters to multiple GPUs and enables to deploy a big model. However, MP is often used with DP because MP-only solution is also not scalable due to (1) increasing communication overhead between model-parallel ranks and (2) decreasing per-rank data parallelism. Therefore, given a multi-node training system, it is ideal to minimize the use of MP and deploy the model on rest of GPUs using DP. As long as using DP, the memory overhead from parameter duplication still exits and this leads to sub-optimal parallelism (e.g., smaller per-GPU batch and more model splits across GPUs).

---

## Contributions

- The authors first propose __ZeRO-DP__, the solution to remove memory redundancy among data-parallel ranks. ZeRO-DP partitions (1) optimizer states, (2) gradients, and (3) parameters across data-parallel ranks and achieves linear memory saving with the increasing number of GPUs in the training system.

- As the solution to save the residual state memory usage per GPU, the authors propose __ZeRO-R__. ZeRO-R uses (1) activations checkpoint, (2) activations off-loading to system memory, (3) improved temporal buffer memory, and (4) less memory fragmentation with pre-allocation.

---

## Main ideas explained

### ZeRO-DP
I think ZeRO-DP is the key of this paper as the ideas are focused on a large language model where the model parameter-associated memory allocation dominates the memory usage. Language models are known to work well with mixed-precision (ref) and, assuming this training mode, training needs memory for 5 copies of parameters; model parameters, master parameters, parameter gradients, and optimizer states (optimizer needs 2X copies of parameters assuming Adam). Among these, master parameters and optimizer states are maintained in fp32 and the rest are in fp16. When deploying a model with 10B parameters, 

### ZeRO-R


---

## Key results

- xxxx
- xxxx

---

## My thoughts and potential follow-ups

- xxxx
- xxxx


Reference...