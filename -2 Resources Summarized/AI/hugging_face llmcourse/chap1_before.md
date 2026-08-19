NLP (Natural Language Processing) is the broader field focused on enabling computers to understand, interpret, and generate human language. NLP encompasses many techniques and tasks such as sentiment analysis, named entity recognition, and machine translation.
 LLMs (Large Language Models) are a powerful subset of NLP models characterized by their massive size, extensive training data, and ability to perform a wide range of language tasks with minimal task-specific training. Models like the Llama, GPT, or Claude series are examples of LLMs that have revolutionized what’s possible in NLP.

A large language model (LLM) is an AI model trained on massive amounts of text data that can understand and generate human-like text, recognize patterns in language, and perform a wide variety of language tasks without task-specific training. They represent a significant advancement in the field of natural language processing (NLP).

LLMs are characterized by:
- **Scale**: They contain millions, billions, or even hundreds of billions of parameters
- **General capabilities**: They can perform multiple tasks without task-specific training
- **In-context learning**: They can learn from examples provided in the prompt
- **Emergent abilities**: As these models grow in size, they demonstrate capabilities that weren’t explicitly programmed or anticipated
However, LLMs also have important limitations:

- **Hallucinations**: They can generate incorrect information confidently
- **Lack of true understanding**: They lack true understanding of the world and operate purely on statistical patterns
- **Bias**: They may reproduce biases present in their training data or inputs.
- **Context windows**: They have limited context windows (though this is improving)
- **Computational resources**: They require significant computational resources

The 🤗 Transformers library provides the functionality to create and use those shared models


The most basic object in the 🤗 Transformers library is the `pipeline()` function. It connects a model with its necessary preprocessing and postprocessing steps, allowing us to directly input any text and get an intelligible answer

Base class implementing pipelined operations. Pipeline workflow is defined as a sequence of the following
    operations:
		Input -> Tokenization -> Model Inference -> Post-Processing (task dependent) -> Output


There are three main steps involved when you pass some text to a pipeline:

	the text is preprocessed into a format the model can understand.
    The preprocessed inputs are passed to the model.
    The predictions of the model are post-processed, so you can make sense of them.
Text pipelines

    text-generation: Generate text from a prompt
    text-classification: Classify text into predefined categories
    summarization: Create a shorter version of a text while preserving key information
    translation: Translate text from one language to another
    zero-shot-classification: Classify text without prior training on specific labels
    feature-extraction: Extract vector representations of text

Image pipelines

    image-to-text: Generate text descriptions of images
    image-classification: Identify objects in an image
    object-detection: Locate and identify objects in images

Audio pipelines

    automatic-speech-recognition: Convert speech to text
    audio-classification: Classify audio into categories
    text-to-speech: Convert text to spoken audio

Multimodal pipelines

    image-text-to-text: Respond to an image based on a text prompt


if we need to classify texts that haven’t been labelled. This is a common scenario in real-world projects because annotating text is usually time-consuming and requires domain expertise. For this use case, the zero-shot-classification pipeline is very powerful: it allows you to specify which labels to use for the classification, so you don’t have to rely on the labels of the pretrained model. You’ve already seen how the model can classify a sentence as positive or negative using those two labels — but it can also classify the text using any other set of labels you like.


The top_k argument controls how many possibilities you want to be displayed. Note that here the model fills in the special <mask> word, which is often referred to as a mask token. Other mask-filling models might have different mask tokens, so it’s always good to verify the proper mask word when exploring other models. One way to check it is by looking at the mask word used in the widget.

Named entity recognition (NER) is a task where the model has to find which parts of the input text correspond to entities such as persons, locations, or organizations.

We pass the option grouped_entities=True in the pipeline creation function to tell the pipeline to regroup together the parts of the sentence that correspond to the same entity: here the model correctly grouped “Hugging” and “Face” as a single organization, even though the name consists of multiple words. In fact, as we will see in the next chapter, the preprocessing even splits some words into smaller parts. For instance, Sylvain is split into four pieces: S, ##yl, ##va, and ##in. In the post-processing step, the pipeline successfully regrouped those pieces.

