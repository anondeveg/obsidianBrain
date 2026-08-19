

## 1. Self-Supervised Learning

**Self-supervised learning** trains a model using targets that are **automatically created from the input data itself**.

No human needs to label the data.

Example:

> The cat is sitting on the mat.

Hide a word:

> The cat is sitting on the ___.

The original sentence provides the target:

$$
\text{Input} = \text{“The cat is sitting on the ___”}
$$

$$
\text{Target} = \text{“mat”}
$$

So the model learns from the data itself.

### Self-supervised vs. unsupervised

|              | Unsupervised    | Self-supervised               |
| ------------ | --------------- | ----------------------------- |
| Human labels | No              | No                            |
| Target       | Not necessarily | Automatically created         |
| Example      | Clustering      | Predicting masked/next tokens |

The key idea:

$$
\boxed{\text{Self-supervised learning = supervision generated from the data itself}}
$$

---

# 2. Pretraining

A model trained with self-supervision develops a **statistical understanding of the language** it was trained on.

However, this general knowledge isn't necessarily optimized for a particular practical task.

This is where **pretraining and fine-tuning** come in.

### Pretraining

**Pretraining** means training a model **from scratch**:

* weights start randomly initialized
* the model has no prior knowledge
* it learns from a large dataset

$$
\boxed{\text{Random weights} \rightarrow \text{training on large data} \rightarrow \text{pretrained model}}
$$

---

# 3. Fine-Tuning / Transfer Learning

After pretraining, the model can be trained further for a specific task.

This is **fine-tuning**.

For example, you might take a pretrained language model and train it for a particular classification task using human-annotated data.

The important advantage is that the model **already learned something about language during pretraining**.

Therefore, fine-tuning:

* requires much less data
* requires less time
* requires fewer resources

than training the model from scratch for the final task.

So the general process is:

$$
\boxed{
\text{Pretraining}
\rightarrow
\text{general language knowledge}
\rightarrow
\text{Fine-tuning}
\rightarrow
\text{specific task}
}
$$

---

# 4. Two Examples of Language Modeling

### Causal Language Modeling

The model predicts the **next word/token** using the previous ones.

For example:

> The cat is sitting on the ...

The model predicts the next token based on what came before it.

It is called **causal** because the output depends on the **past and present**, not the future.

$$
\text{past + present} \rightarrow \text{next token}
$$

---

### Masked Language Modeling

A word/token is hidden, and the model predicts it.

> The cat is sitting on the `[MASK]`.

$$
\text{surrounding context} \rightarrow \text{masked token}
$$

These are two different ways of training language models.

---

# 5. Transformers and Model Size

Transformers can be very large.

Generally, increasing:

* the **model size**
* the amount of **pretraining data**

can improve performance.

However, larger models and more training also require more computational resources and can have a larger **environmental/carbon footprint**.

The course mentions tools such as **ML CO₂ Impact** and **CodeCarbon** for estimating the carbon footprint of model training.

---

# 6. Encoder vs. Decoder

A Transformer can have an **encoder**, a **decoder**, or both.

### Encoder

The encoder receives an input and builds a **numerical representation** of that input.

Think:

$$
\boxed{\text{Input} \rightarrow \text{features/representation}}
$$

It is optimized toward **understanding the input**.

### Decoder

The decoder uses the encoder's representation, along with other inputs, to **generate a target sequence**.

Think:

$$
\boxed{\text{features + other inputs} \rightarrow \text{output}}
$$

---

# 7. Three Transformer Types

### Encoder-only

Good for tasks requiring understanding of the input.

Examples:

* sentence classification
* named entity recognition

### Decoder-only

Good for **generation**.

Example:

* text generation

### Encoder-decoder

Also called **sequence-to-sequence** models.

Good when you have an input and need to generate an output.

Examples:

* translation
* summarization

---

# 8. Attention

**Attention** is a key component of Transformers.

Its basic purpose is to allow the model to **focus on relevant words when processing a particular word**.

For example, translating:

> You like this course.

When processing **“like”**, knowing the subject **“You”** is important because the French verb depends on the subject.

When processing **“this”**, the model needs information about **“course”**, because the translation can depend on the associated noun.

So attention helps the model determine:

> **Which other words are important for understanding this word?**

A useful mental model is:

$$
\boxed{\text{Attention = deciding which parts of the input are relevant}}
$$

The Transformer architecture was originally designed for **translation**, where this ability is particularly useful.

---

# 9. Attention in the Encoder vs. Decoder

There is an important difference.

### Encoder

The encoder can use **all words in the input sentence**.

For example:

> You like this course.

When processing a word, it can consider words both **before and after** it.

This makes sense because the meaning/translation of a word can depend on later words too.

### Decoder

The decoder generates the output **sequentially**.

Therefore, when generating a word, it can only use the target words it has already generated.

For example, if it has generated the first three translated words:

$$
w_1,\quad w_2,\quad w_3
$$

it uses those words, along with the encoder's input representation, to predict:

$$
w_4
$$

It cannot look at the future target word $w_5$ because it hasn't generated it yet.

---

# 10. Architecture vs. Checkpoint vs. Model

These terms are easy to mix up.

### Architecture

The **skeleton/structure** of the model:

* layers
* operations
* how everything is connected

### Checkpoint

The **trained weights** that are loaded into an architecture.

For example:

`bert-base-cased`

is a particular set of trained BERT weights.

### Model

A general term that can refer to either the architecture or checkpoint.

So:

$$
\boxed{
\text{Architecture} = \text{structure}
}
$$

$$
\boxed{
\text{Checkpoint} = \text{trained weights}
}
$$

---

# The Whole Picture

You can connect the concepts like this:

$$
\boxed{
\text{Large unlabeled dataset}
\rightarrow
\text{Self-supervised pretraining}
\rightarrow
\text{Pretrained model}
}
$$

Then:

$$
\boxed{
\text{Pretrained model}
\rightarrow
\text{Fine-tuning}
\rightarrow
\text{Specific task}
}
$$

And the Transformer itself can be organized as:

$$
\boxed{
\text{Encoder}
\quad|\quad
\text{Decoder}
\quad|\quad
\text{Encoder + Decoder}
}
$$

with **attention** helping the model determine which parts of its available context are relevant.

---

# Q&A Review

**Q: What is self-supervised learning?**
A: Training where the targets are automatically obtained from the input data.

**Q: Does self-supervised learning require humans to label the data?**
A: No.

**Q: What is pretraining?**
A: Training a model from scratch, starting with randomly initialized weights.

**Q: What is fine-tuning?**
A: Further training of a pretrained model on data specific to a task.

**Q: Why fine-tune instead of training from scratch?**
A: The pretrained model already has useful knowledge, so fine-tuning needs less data, time, and resources.

**Q: What is causal language modeling?**
A: Predicting the next token using previous tokens.

**Q: What is masked language modeling?**
A: Predicting a token that has been masked.

**Q: What does an encoder do?**
A: Builds a numerical representation of the input.

**Q: What does a decoder do?**
A: Generates an output sequence using representations and other inputs.

**Q: What are encoder-only models good for?**
A: Understanding tasks such as classification and named entity recognition.

**Q: What are decoder-only models good for?**
A: Generative tasks such as text generation.

**Q: What are encoder-decoder models good for?**
A: Sequence-to-sequence tasks such as translation and summarization.

**Q: What does attention do?**
A: It lets the model focus on relevant words when processing a particular word.

**Q: Can the encoder see future words in its input?**
A: Yes, the encoder can use all words in the input.

**Q: Can the decoder see future target words?**
A: No. It generates sequentially and can only use the target words already generated.

**Q: What is an architecture?**
A: The structure of the model—its layers and operations.

**Q: What is a checkpoint?**
A: A set of trained weights loaded into an architecture.

**Q: What is BERT in this terminology?**
A: An architecture.

**Q: What is the simplest way to remember architecture vs. checkpoint?**

$$
\boxed{\text{Architecture = how it's built}}
$$

$$
\boxed{\text{Checkpoint = what it has learned}}
$$
