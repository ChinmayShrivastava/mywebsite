---
title: Random thoughts
author: Chinmay Shrivastava
pubDatetime: 2024-11-20T04:06:31Z
slug: random-thoughts-001
featured: true
draft: false
tags:
  - AI
  - Optimization
  - Sustainability
  - Mesh Optimization
  - Mechanical Design
  - FEM
description: A collection of random thoughts on the intersection of AI and mechanical design.
---

## Table of contents

A foundational model trained on mechanical data should aid the optimization process, resulting in designs using a lot less material and improving mechanical performance. I am fundamentally interested in exploring these capabilities of such a model to potentially avoid waste and improve intrinsic performance of these autonomously optimized mechanical designs.

Over the last two years I have closely studied knowledge graphs and transformer models, fine tuned them for specific use cases involving but not only layout parsing for effective website automation, and learning recommendation. I have also built several applications involving effective knowledge graph based RAG, most notable of which was building an ontology of learning concepts to generate personalized learning recommendations trained on ~500K documents from across the internet. All combined, my applications were put in the hands of more than 1200 users and generated a revenue of ~25K USD.

Through my foundational understanding of concepts from knowledge graphs, I understand effective management of the plethora of variables that can play a deciding role in optimization processes. In mechanical optimization, everything from selection of the right material, to the right parts, joints and the choice of simulations can affect the final output for better or worse. Most of a mechanical optimization engineer’s job still revolves around these basic decisions, spending months iterating over and optimizing designs. Yet, two experts working on the same problem in isolation, more likely than not, will come up with different results.

With hardware enabled acceleration of advanced intelligent models, and contemporary availability of historical–physics informed–labeled data, models can be built to perform these optimization tasks much faster and cheaper. The optimized designs thus obtained, and generated over thousands if not millions of iterations will account for every variable, reduce waste and enhance every mechanical property in a way no unenhanced human can.

My initial foray is in collating these variables and studying existing frameworks (mostly open source) and starting by fine-tuning a language model (as opposed to training a whole foundational model for design optimization) to effectively optimize meshes through generative discrete finite element optimization. Preliminary research performed in this direction has already borne fruit. Nvidia’s LLaMA-Mesh effectively generates meshes from natural language descriptions. Mesh-to-mesh generation through fine-tuned language models as a next step will set a precedent for upcoming design optimization models, most of which will benefit from state-space search.

I anchor my inspiration in Maurice Conti’s 2017 Ted Talk titled “The incredible inventions of intuitive AI” among other influential research in the domain. Over the course of the video he mentions optimizing the chassis of a car through collecting hours of mechanical data and training an optimization model to iteratively update the chassis to save material and maximize performance. I am also inspired by Mamba (Gu, Dao 2023) that uses space state to model linear time sequences, eliminating limitations of the Transformer architecture, LLMs as optimizers (Yang, Chen 2024) that recursively use LLMs to optimize themselves through a simple beam search in the latent space, and it's more theorized version, Textual Gradient Descent (Pryzant 2023).

I believe these advances in higher throughput models and automatic optimization lead up to optimizing 3D spaces as well. I have long been interested in sustainability and believe that faster and better designs can fundamentally lead to huge energy savings impacting positively to the environment around us.
