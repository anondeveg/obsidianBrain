
## Introduction to NLP and LLMs

NLP (Natural Language Processing) is the broader field focused on enabling computers to understand, interpret, and generate human language. NLP encompasses many techniques and tasks such as sentiment analysis, named entity recognition, and machine translation.

A Large Language Model (LLM) is an AI model trained on massive amounts of text data that can understand and generate human-like text, recognize patterns in language, and perform a wide variety of language tasks without task-specific training. Models like the Llama, GPT, or Claude series are examples of LLMs that have revolutionized what’s possible in NLP.

**Characteristics of LLMs:**

* **Scale:** They contain millions, billions, or even hundreds of billions of parameters.


* **General capabilities:** They can perform multiple tasks without task-specific training.


* **In-context learning:** They can learn from examples provided in the prompt.


* **Emergent abilities:** As these models grow in size, they demonstrate capabilities that weren’t explicitly programmed or anticipated.



**Limitations of LLMs:**

* **Hallucinations:** They can generate incorrect information confidently.


* **Lack of true understanding:** They lack true understanding of the world and operate purely on statistical patterns.


* **Bias:** They may reproduce biases present in their training data or inputs.


* **Context windows:** They have limited context windows (though this is improving).


* **Computational resources:** They require significant computational resources.



---

## The 🤗 Transformers Library

The 🤗 Transformers library provides the functionality to create and use those shared models. The most basic object in the library is the `pipeline()` function. It connects a model with its necessary preprocessing and postprocessing steps, allowing us to directly input any text and get an intelligible answer.

The pipeline workflow is defined as a sequence of the following operations: Input -> Tokenization -> Model Inference -> Post-Processing (task dependent) -> Output.

There are three main steps involved when you pass some text to a pipeline:

1. The text is preprocessed into a format the model can understand.


2. The preprocessed inputs are passed to the model.


3. The predictions of the model are post-processed, so you can make sense of them.



---

## Types of Pipelines

The 🤗 Transformers library supports a variety of specialized pipelines across different modalities:

**Text Pipelines:**

* **text-generation:** Generate text from a prompt.


* **text-classification:** Classify text into predefined categories.


* **summarization:** Create a shorter version of a text while preserving key information.


* **translation:** Translate text from one language to another.


* **zero-shot-classification:** Classify text without prior training on specific labels.


* **feature-extraction:** Extract vector representations of text.



**Image Pipelines:**

* **image-to-text:** Generate text descriptions of images.


* **image-classification:** Identify objects in an image.


* **object-detection:** Locate and identify objects in images.



**Audio Pipelines:**

* **automatic-speech-recognition:** Convert speech to text.


* **audio-classification:** Classify audio into categories.


* **text-to-speech:** Convert text to spoken audio.



**Multimodal Pipelines:**

* **image-text-to-text:** Respond to an image based on a text prompt.



---

## Hands-On Python Examples

To execute these pipelines in a Python environment, you must first install the required libraries:

```python
!pip install datasets evaluate transformers[sentencepiece]

```

### 1. Zero-Shot Classification

The zero-shot-classification pipeline is very powerful if we need to classify texts that haven’t been labelled. This is a common scenario in real-world projects because annotating text is usually time-consuming and requires domain expertise. It allows you to specify which labels to use for the classification, so you don’t have to rely on the labels of the pretrained model.

```python
from transformers import pipeline

classifier = pipeline("zero-shot-classification")
classifier(
    "donald trump is the teacher and president of the united states of america",
    candidate_labels=["education", "politics", "business"],
)

```

(Code source:)

### 2. Text Generation

You can use specialized models, such as `AxiomicLabs/GPT-X2.5-135M`, to generate text based on a short input prompt.

```python
from transformers import pipeline

generator = pipeline("text-generation",model="AxiomicLabs/GPT-X2.5-135M")
result = generator("omar is ", max_length=30)
print(result)

```

(Code source:)

### 3. Fill-Mask

The model fills in the special `<mask>` word, which is often referred to as a mask token. The `top_k` argument controls how many possibilities you want to be displayed. Other mask-filling models might have different mask tokens, so it’s always good to verify the proper mask word when exploring other models.

```python
from transformers import pipeline

unmasker = pipeline("fill-mask")
unmasker("sisi the presidint of <mask> which is in top right africa", top_k=2)

```

(Code source:)

### 4. Named Entity Recognition (NER)

Named entity recognition (NER) is a task where the model has to find which parts of the input text correspond to entities such as persons, locations, or organizations.

During tokenization, preprocessing even splits some words into smaller parts (for instance, "Sylvain" is split into four pieces: "S", "##yl", "##va", and "##in"). We can pass options like `grouped_entities=True` (or `aggregation_strategy="simple"`) to tell the pipeline to regroup together the parts of the sentence that correspond to the same entity during the post-processing step.

```python
from transformers import pipeline

ner = pipeline("ner", aggregation_strategy="simple")
ner("lucas is the presdint of Egypt")

```

(Code source:)

### 5. Question Answering and Summarization

(Note: Depending on your specific Transformers library version or environment setup, calling these standard pipelines might result in a `KeyError` if the task is unrecognized or models are missing).

```python
from transformers import pipeline

# Question Answering
question_answerer = pipeline("question-answering")
question_answerer(
    question="will i get 100% in my next college semester?",
    context="i will get it 100%",
)

# Summarization
summarizer = pipeline("summarization")
summarizer(
    """
    America has changed dramatically during recent years. Not only has the number of
    graduates in traditional engineering disciplines such as mechanical, civil,
    electrical, chemical, and aeronautical engineering declined, but in most of
    the premier American universities engineering curricula now concentrate on
    and encourage largely the study of engineering science. As a result, there
    are declining offerings in engineering subjects dealing with infrastructure,
    the environment, and related issues, and greater concentration on high
    technology subjects, largely supporting increasingly complex scientific
    developments. While the latter is important, it should not be at the expense
    of more traditional engineering.

    Rapidly developing economies such as China and India, as well as other
    industrial countries in Europe and Asia, continue to encourage and advance
    the teaching of engineering. Both China and India, respectively, graduate
    six and eight times as many traditional engineers as does the United States.
    Other industrial countries at minimum maintain their output, while America
    suffers an increasingly serious decline in the number of engineering graduates
    and a lack of well-educated engineers.
"""
)

```

(Code source:)