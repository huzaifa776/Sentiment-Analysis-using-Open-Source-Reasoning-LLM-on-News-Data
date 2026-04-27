# Sentiment Analysis using Open Source Reasoning LLM on News Data

An end-to-end notebook project that loads a news dataset from Hugging Face, prepares inputs, runs a reasoning-capable LLM (DeepSeek R1 Distill Qwen 1.5B) with 4-bit quantization, and exposes a Gradio UI for interactive sentiment analysis. The notebook prints concise reasoning, sentiment label, and a topic tag for each news item.

## Project Contents

- Notebook: [Sentiment_Analysis.ipynb](Sentiment_Analysis.ipynb)
- README: [readme.md](readme.md)

## What This Project Does

- Installs required libraries in the notebook environment.
- Authenticates with Hugging Face to access model assets.
- Loads the news dataset from the Hugging Face Hub.
- Combines title and text into a single promptable field.
- Loads a quantized LLM and tokenizer for inference.
- Builds a prompt template that requests reasoning, sentiment, and tag.
- Runs inference with a text-generation pipeline.
- Provides a Gradio interface to fetch random items and analyze them.

## Requirements

- macOS or Linux recommended (Windows should also work).
- Python 3.9+.
- GPU strongly recommended for inference; CPU will be very slow.
- A Hugging Face account and access token.

## Quick Start

1. Open the notebook [Sentiment_Analysis.ipynb](Sentiment_Analysis.ipynb) in Jupyter or VS Code.
2. Run Cell 1 to install dependencies.
3. Run Cell 2 to log in to Hugging Face.
4. Run Cells 3-13 to load data, the model, and set up the pipeline.
5. Run Cells 14-19 to test prompting and sentiment analysis.
6. Run Cell 20 to launch the Gradio interface.

## Notebook Walkthrough

The notebook is organized into these sections:

1. Install and login
	- Installs `transformers`, `accelerate`, `bitsandbytes`, `torch`, `datasets`, `gradio`.
	- Runs Hugging Face login to access the model.

2. Data loading and preparation
	- Loads `fdaudens/ai-jobs-news-articles` from Hugging Face Datasets.
	- Builds a `full_text` field by combining title and text for each item.

3. Model setup
	- Loads `deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B` with 4-bit quantization.
	- Initializes the tokenizer and text-generation pipeline.

4. Prompting and parsing
	- Uses a template that requests:
	  - REASONING (brief, 1-2 points)
	  - SENTIMENT (Positive, Negative, Neutral)
	  - TAG (1-3 words)
	- Parses the output into a formatted response.

5. Testing
	- Runs the model on a few random samples and displays results.

6. Gradio UI
	- Fetches random news items.
	- Runs sentiment analysis from the UI.
	- Shows model reasoning and output in collapsible panels.

## Configuration

You can adjust these settings in the notebook:

- Dataset: `dataset_id` in the data loading cell.
- Model: `model_id` in the model loading cell.
- Generation parameters:
  - `max_new_tokens`
  - `temperature`
  - `top_p`

## Notes on Performance

- The model is loaded with 4-bit quantization using BitsAndBytes.
- If you are on CPU, expect long inference times.
- On GPU, inference should be significantly faster.

## Troubleshooting

- If Hugging Face login fails, ensure your token has read access.
- If CUDA is not detected, verify your GPU runtime setup.
- If the model download is slow, check your network and cache location.

## Example Output Format

The model is prompted to return three lines only:

```
REASONING: <short financial reasoning>
SENTIMENT: Positive|Negative|Neutral
TAG: <topic tag>
```

## License

Specify your license here (for example, MIT). If you are unsure, leave this section as a placeholder or remove it.

## Acknowledgments

- Hugging Face Transformers and Datasets
- DeepSeek R1 Distill Qwen model
- Gradio for the interactive UI
