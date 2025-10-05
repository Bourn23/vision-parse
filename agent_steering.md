# Project Summary

This project, `vision-parse`, is a Python library designed to extract content from PDF files and convert it into markdown format. It leverages vision-capable Large Language Models (LLMs) to analyze images of PDF pages and generate structured text.

## Core Components

The two main components of this project are `parser.py` and `llm.py`.

### `parser.py`

This file contains the `VisionParser` class, which serves as the primary interface for the library. Its responsibilities include:

- **PDF Processing**: It accepts a path to a PDF file.
- **Image Conversion**: Using the `pypdfium2` library, it converts each page of the PDF into a high-resolution image.
- **Batching and Concurrency**: It can process multiple pages concurrently to speed up the extraction process.
- **LLM Interaction**: It orchestrates the process of sending these images to the `LLM` class for analysis and markdown generation.

### `llm.py`

This file houses the `LLM` class, which handles all interactions with the underlying Large Language Models. Its key functions are:

- **Multi-Provider Support**: It supports various LLM providers, including Ollama, OpenAI (and Azure OpenAI), and Gemini.
- **Prompt Engineering**: It constructs specific prompts to guide the LLM in its analysis of the page images.
- **Detailed Extraction**: It has an optional two-step process. First, it can perform a detailed analysis of the image to identify elements like text, tables, and equations. Second, it uses this analysis to generate a more accurate and structured markdown output.
- **API Communication**: It manages the API calls to the selected LLM provider, sending the image data and receiving the generated markdown.

## Workflow

1.  A user provides a PDF file to the `VisionParser`.
2.  The `VisionParser` iterates through the PDF, converting each page into an image.
3.  For each image, the `VisionParser` calls the `LLM` class.
4.  The `LLM` class sends the image to the configured vision model (e.g., LLaVA, GPT-4o, or Gemini).
5.  The model returns a markdown representation of the page content.
6.  The `VisionParser` collects the markdown from all pages and returns it to the user.