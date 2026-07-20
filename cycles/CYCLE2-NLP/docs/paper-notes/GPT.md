# Improving Language Understanding by Generative Pre-Training Notes
> July 17th, 2026
## Why I Read It
I read this paper to understand the underlying structure and architecture of GPT.

I found that I could apply my knowledge of attention and transformers on this paper and understand it thoroughly.

## Context
- Using inlabeled data can reduce time and costs and can increase performance on NLP tasks
- The 2 main difficulties in leveraging unlabeled data are:
    - Unclear optimization for a specific task
    - Unclear transfer learning

We cant keep pretraining from sratch for each specific task, so instead OpenAI proposed a new strategy

## Core Idea

The core idea of this paper was a simple 2 step process that OpenAI proposed: 

1. Generative, unsupervised pretraining 
2. Supervised fine-tuning for a specific task

The paper kept refering back to this structure and on 9 out of 12 datasets, it produced better results than leading models

## Architecture

**Unsupervised pretraining**:

- Multi-layer **transformer decoder** for language model
- Multihead self attention (proposed in Attention is all you need)
- Operation over the input conext tokens followed by a position-wise feedforward layers produce an output distribution over large tokens

**Supervised fine-tuning**:

- After training the model on a large corpus of text, we need to adapt the parameters to the supervised target task 
- We then use dataset C, which is labeled, to pass through the pretrained model
- Finally we feed that through an addtional linear layer (aka: head) to predict the final output


The researchers also did some task-specific input transformations where they used a traversal-style approach. They converted structured outputs into an ordered sequence that the model can process and made it possible for them to not make extensive changes to the architecture across tasks
## Training Process
In the experiment these were the specific things that they did to the model:
- 12-layer decoder only transformer
- masked self-attention heads
- Adam optimization scheme
- 100 epochs on minibatches of 64 randomly sampled
- Bytepair encoding for tokenization
- Simple initialization of N(0, 0.02)
- L2 Regularization
- For a activation: Gaussian Error Linear Unit (GELU)
- Positional embeddings

Finetuning:
- reuse hyperparameter settings
- dropout of 0.1
- 3 epochs of training was enough
- Linear learning rate decay schedule with warmup over 0.2% of training


## What Surprised Me
This whole paper really just felt like a lot of ideas combined together in a specific way to build what is now called GPT. It was amazing how well thought out this was and how much I understood it.

## Connections to Previous Learning
- Transformers
- Self attention
- Transfer learning
- Tokenization
- Adding heads during finetuning

## Questions I Still Have
- Difference with this architecture and BERT
- How DeepSeek is using reinforcement learning to finetune instead of humans actually needing to supervise and finetune
- Currently, do we need to re-engineer frontier models for them to work and attend to using computers or robotics?

