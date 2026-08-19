# Chapter 1.4: Self-Supervised Learning and Transformers

Self-supervised learning is a type of training in which the objective is automatically computed from the inputs of the model. That means that humans are not needed to label the data!

## Self-Supervised Learning

You also start with unlabeled data, but you create the labels/targets automatically from the data itself.

For example, take:

> "The cat is sitting on the mat."

Hide a word:

> "The cat is sitting on the ___."

The original text tells us the answer is `"mat"`.

So we have automatically created a training example:

$$
\begin{aligned}
\text{Input:} &\quad \text{"The cat is sitting on the \_\_\_"} \\
\text{Target:} &\quad \text{"mat"}
\end{aligned}
$$

No human had to label it. This is essentially how many language models learn.

### The Important Distinction

| Feature | Unsupervised | Self-supervised |
| :--- | :--- | :--- |
| **Human labels?** | No | No |
| **Has a target?** | Not necessarily | Yes |
| **Target comes from** | — | The data itself |
| **Example** | Clustering | Predict masked/next token |

A useful way to remember it:

> **Self-supervised = supervision generated from the data itself.**

This type of model develops a statistical understanding of the language it has been trained on, but it’s less useful for specific practical tasks. Because of this, the general pretrained model then goes through a process called transfer learning or fine-tuning. During this process, the model is fine-tuned in a supervised way — that is, using human-annotated labels — on a given task.

An example of a task is predicting the next word in a sentence having read the n previous words. This is called causal language modeling because the output depends on the past and present inputs, but not the future ones.

Another example is masked language modeling, in which the model predicts a masked word in the sentence.


## Transformers Are Big Models

Apart from a few outliers (like DistilBERT), the general strategy to achieve better performance is by increasing the models’ sizes as well as the amount of data they are pretrained on.

![[Pasted image 20260813214557.png]]

This illustrates a project for a (very big) model led by a team consciously trying to reduce the environmental impact of pretraining. The footprint of running lots of trials to get the best hyperparameters would be even higher.

You can evaluate the carbon footprint of your models’ training through several tools:
- https://mlco2.github.io/impact/#compute
- https://codecarbon.io/

## Pretraining vs Fine-Tuning

**Pretraining** is the act of training a model from scratch: the weights are randomly initialized, and the training بََََ

**Fine-tuning**, on the other hand, is the training done after a model has been pretrained. To perform fine-tuning, you first acquire a pretrained language model, then perform additional training with a dataset specific to your task.

Why not simply train the model for your final use case from scratch?
- The pretrained model was already trained on a dataset that has similarities with the fine-tuning dataset, enabling transfer of learned representations.
- Fine-tuning requires significantly less data to get decent results.
- The amount of time and compute resources needed are dramatically lower.

## Encoder and Decoder

- **Encoder (left)**: The encoder receives an input and builds a numerical representation of it (its features). This means the model is optimized to acquire understanding from the input.
- **Decoder (right)**: The decoder uses the encoder’s representation along with other inputs to generate a target sequence. This means the model is optimized for generating outputs.

![[Pasted image 20260814164311.png]]

Each of these parts can be used independently, depending on the task:
- **Encoder-only models**: Good for tasks that require understanding of the input, such as sentence classification and named entity recognition.
- **Decoder-only models**: Good for generative tasks such as text generation.
- **Encoder-decoder models (sequence-to-sequence)**: Good for generative tasks that require an input, such as translation or summarization.

## Attention Layers

Attention tells the model to give attention to specific words related to the current word it is reading. A key feature of Transformer models is that they are built with special layers called attention layers (“Attention Is All You Need”).

Consider the task of translating text from English to French: Given the input *“You like this course”*, a translation model will need to attend to the adjacent word *“You”* to get the proper translation for the word *“like”* (conjugation in French depends on subject).

## Key Definitions

- **Architecture**: The skeleton of the model — the definition of each layer and each operation that happens within the model.
- **Checkpoints**: The specific trained weights that are loaded into a given architecture.
- **Model**: An umbrella term that can refer to either the architecture or the checkpoint (e.g., BERT is an architecture, while `bert-base-cased` is a checkpoint).