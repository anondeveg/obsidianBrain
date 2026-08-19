https://arxiv.org/pdf/2411.17835

# Arabic-Nougat — Complete Summary

The paper presents **Arabic-Nougat**, an adaptation of the Nougat document-understanding architecture specifically for **Arabic OCR and Markdown/document extraction**.

The core idea is:

$$
\boxed{
\text{Arabic Book Page Image}
\rightarrow
\text{Vision Encoder}
\rightarrow
\text{Transformer Decoder}
\rightarrow
\text{Arabic Markdown}
}
$$

Instead of performing traditional OCR by detecting individual characters, the model learns to directly transform a document image into a sequence of text/Markdown tokens.

---

## 1. The Architecture

Arabic-Nougat uses a **Donut Vision Encoder** together with an **MBART Transformer decoder**.

### Donut Vision Encoder

The encoder receives the page as an image:

$$
I \in \mathbb{R}^{H\times W\times3}
$$

and converts the pixels into visual representations:

$$
I\rightarrow
(\mathbf h_1,\mathbf h_2,\ldots,\mathbf h_n)
$$

You can think of the encoder as the model's **eyes**.

It learns visual information such as:

* Arabic text
* page layout
* headings
* paragraphs
* equations
* document structure

---

## 2. MBART Decoder

The decoder takes those visual representations and generates the output **token by token**.

For example:

```text
<BOS>
↓
#
↓
مقدمة
↓
\n
↓
كان
↓
العرب
↓
...
```

This is called **autoregressive generation**.

Mathematically:

$$
P(y_1,\ldots,y_T|I)
===================

\prod_{t=1}^{T}
P(y_t|y_{<t},I)
$$

In other words:

> Given the image and everything I've generated so far, what token should I generate next?

---

# 3. Attention

**Attention** is the mechanism that allows Transformer tokens to determine which other information is relevant.

The basic equation is:

$$
\operatorname{Attention}(Q,K,V)
===============================

\operatorname{softmax}
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

The three components are:

* $Q$ — **Query:** what information am I looking for?
* $K$ — **Key:** what information do I contain?
* $V$ — **Value:** the actual information to retrieve.

Conceptually:

$$
\boxed{
Q
\rightarrow
\text{compare with }K
\rightarrow
\text{attention weights}
\rightarrow
\text{combine }V
}
$$

---

# 4. Self-Attention vs Cross-Attention

This distinction is important for Arabic-Nougat.

### Self-attention

The decoder looks at its **own previously generated tokens**.

For example:

```text
# مقدمة
   ↑
```

The representation of `مقدمة` can use information from `#`.

### Cross-attention

The decoder looks at the **visual features produced by Donut**.

```text
Book Image
    ↓
Donut
    ↓
Visual Features
    ↓
Cross-Attention ← MBART Decoder
    ↓
Next Token
```

This allows the decoder to effectively ask:

> "Which part of the page is relevant to the token I'm generating?"

---

# 5. Is MBART bidirectional?

**Partially.**

MBART is an **encoder-decoder Transformer**.

```text
             MBART
               │
       ┌───────┴───────┐
       ↓               ↓
    Encoder         Decoder
       │               │
  Bidirectional    Autoregressive
```

The **encoder** can use information from both directions:

$$
\text{left context}+\text{token}+\text{right context}
$$

The **decoder** generates left-to-right:

$$
y_1\rightarrow y_2\rightarrow y_3\rightarrow\cdots
$$

This is useful because understanding existing information benefits from seeing the whole context, while generation must happen sequentially.

---

# 6. Arabic Base Nougat

The paper introduces an Arabic Base model obtained by **fine-tuning `nougat-base` on Arabic data**.

Conceptually:

$$
\text{Nougat Base}
+
\text{Arabic training data}
\rightarrow
\text{Arabic Base Nougat}
$$

It supports sequences of up to approximately:

$$
4096\text{ tokens}
$$

It uses:

### BF16

`torch.bfloat16` is a **16-bit floating-point representation**.

Compared with FP32:

$$
32\text{ bits}\rightarrow16\text{ bits}
$$

This significantly reduces memory requirements for many computations.

### Flash Attention 2

Flash Attention 2 is an **optimized implementation of Transformer attention**.

It doesn't fundamentally change the attention equation.

Instead, it calculates attention much more efficiently in GPU memory.

This is especially useful for long sequences because normal attention has roughly:

$$
O(N^2)
$$

pairwise interactions for sequence length $N$.

---

# 7. Arabic Large Nougat

The Large version goes further.

It uses:

1. **A larger/expanded Transformer decoder**
2. **Aranizer-PBE-86k tokenizer**
3. Longer effective sequences

### Aranizer-PBE-86k

This is an Arabic-specific tokenizer.

The `86k` refers to roughly:

$$
86,000
$$

vocabulary entries.

A tokenizer converts text into tokens:

$$
\text{text}
\rightarrow
\text{tokens}
\rightarrow
\text{token IDs}
$$

An Arabic-specific tokenizer can represent Arabic text more efficiently than a poorly suited general tokenizer.

---

# 8. Why the tokenizer matters so much

Suppose one tokenizer represents some text as:

```text
Token Token Token Token
Token Token Token Token
```

while another represents the same information as:

```text
Token
Token
```

The second tokenizer is more efficient.

That means more actual Arabic text can fit into the same sequence length.

The paper describes Aranizer as giving roughly **4× the text efficiency** of the previous tokenization.

Thus, approximately:

$$
8192\times4
\approx
32768
$$

So the model has around:

$$
8192
$$

Aranizer tokens, but those can represent an amount of Arabic text roughly comparable to **32k tokens under the older tokenizer**.

The distinction is important:

> It does **not** literally mean the model has a 32,768-token context window.

It means its tokenizer packs approximately that much text into its available token budget.

---

# 9. Why Large is better for Arabic books

Arabic books can contain very long and dense pages.

If your tokenizer is inefficient:

$$
\text{page}
\rightarrow
\text{too many tokens}
\rightarrow
\text{sequence limit}
$$

You may lose part of the output.

With a more efficient Arabic tokenizer:

$$
\text{page}
\rightarrow
\text{fewer tokens}
\rightarrow
\text{more text fits}
$$

This is particularly valuable for **long-form Arabic OCR**.

---

# 10. Markdown Extraction

Arabic-Nougat isn't necessarily trying to produce only raw OCR text.

It can produce structured Markdown.

For example, an image might contain:

```text
الفصل الرابع

مقدمة

كان العلماء...
```

The model can produce:

```markdown
# الفصل الرابع

## مقدمة

كان العلماء...
```

So it learns:

$$
\boxed{
\text{image}
\rightarrow
\text{Arabic text + document structure}
}
$$

rather than merely:

$$
\text{image}
\rightarrow
\text{characters}
$$

This is one of the major advantages of a document-understanding model.

---

# 11. TER — how they measure performance

The paper reports:

$$
TER_{\text{Large}}=1.05
$$

versus:

$$
TER_{\text{Small}}=1.25
$$

**TER = Translation Edit Rate.**

It measures approximately how many edits are required to transform the model's output into the correct reference.

The edits include things such as:

* insertion
* deletion
* substitution
* shifting

Conceptually:

$$
TER
\approx
\frac{\text{number of required edits}}
{\text{reference length}}
$$

**Lower is better.**

Therefore:

$$
1.05 < 1.25
$$

means Arabic Large Nougat's output required fewer corrections.

The paper attributes the improved efficiency partly to its **more advanced Arabic tokenizer**.

---

# 12. Why BF16 + Flash Attention 2 matters

The paper also says that training with:

$$
\boxed{\text{BF16 + Flash Attention 2}}
$$

reduced memory usage.

That has an important practical consequence:

$$
\text{less GPU memory}
\rightarrow
\text{larger batch size}
\rightarrow
\text{more samples processed at once}
$$

and potentially:

$$
\rightarrow
\text{faster training/processing}
$$

So these aren't improvements to the model's Arabic understanding directly. They are primarily **computational optimizations** that make training and inference more practical.

---

# 13. The whole Arabic-Nougat system

You can now put everything together:

```text
                 Arabic Book Page
                        │
                        ▼
              ┌──────────────────┐
              │ Donut Vision     │
              │ Encoder           │
              └────────┬─────────┘
                       │
                 Visual Features
                       │
                       ▼
              ┌──────────────────┐
              │ MBART Transformer│
              │ Decoder           │
              │                  │
              │ Self-Attention   │
              │ Cross-Attention  │
              │ Feed-Forward     │
              └────────┬─────────┘
                       │
                Autoregressive
                  generation
                       │
                       ▼
              Arabic Token IDs
                       │
                       ▼
                   Markdown
```

For **Arabic Large Nougat**, the decoder is expanded and the tokenizer is replaced with **Aranizer-PBE-86k**, allowing much more Arabic text to fit into the sequence.

---

# 14. Base vs Large

|                         | Arabic Base Nougat        | Arabic Large Nougat     |
| ----------------------- | ------------------------- | ----------------------- |
| Starting point          | `nougat-base` fine-tune   | Larger/new architecture |
| Decoder                 | Smaller                   | Expanded                |
| Tokenizer               | Original Nougat tokenizer | Aranizer-PBE-86k        |
| Vocabulary              | Original                  | ~86k                    |
| Sequence                | ~4096 tokens              | ~8192 Aranizer tokens   |
| Effective text capacity | Lower                     | ~32k-token equivalent   |
| BF16                    | Yes                       | Yes                     |
| Flash Attention 2       | Yes                       | Yes                     |
| TER                     | ~1.25                     | **~1.05**               |

---

# The core takeaway

If you remember only **five things**, remember these:

1. **Donut** is the vision encoder — it turns the page image into visual representations.

2. **MBART** is the Transformer decoder — it generates Arabic/Markdown tokens from those visual representations.

3. **Attention** lets the Transformer determine which pieces of information are relevant to each token.

4. **Aranizer-PBE-86k** is an Arabic tokenizer designed to represent Arabic text efficiently, allowing much more text to fit into the model's sequence.

5. **Arabic Large Nougat** improves on the Base model by using a larger decoder and more efficient tokenization, achieving a lower TER of **1.05 vs 1.25**, while BF16 + Flash Attention 2 make the model more memory-efficient to train.

The entire idea can be reduced to:

$$
\boxed{
\text{Image}
\xrightarrow{\text{Donut}}
\text{Visual Features}
\xrightarrow{\text{Transformer + Attention}}
\text{Arabic Tokens}
\xrightarrow{\text{Tokenizer}}
\text{Markdown}
}
$$
z