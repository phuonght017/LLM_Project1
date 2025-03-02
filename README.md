# Summarization Project

This project crawls website content and summarizes it using OpenAI's GPT-4o-mini model.

## 🚀 Setup Environment

### 1. Install Conda
If you haven't installed Conda, download and install it from [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/).

### 2. Create Conda Virtual Environment
```bash
conda env create -f environment.yml
conda activate llms
```

### 3. Install ChromeDriver
On macOS:
```bash
brew install chromedriver
```

On Ubuntu/Debian:
```bash
sudo apt update && sudo apt install -y chromium-chromedriver
```

On Windows:
1. Download ChromeDriver from [here](https://sites.google.com/chromium.org/driver/).
2. Extract and place `chromedriver.exe` in a directory included in your system's PATH.

## 📜 Web Summarization Code

### 1. `Website` Class (Crawling Data)
This class is responsible for fetching website content. Class `selenium` and `ChromeDriver` are used to crawl Javascript-rendered dynamic contents.

#### Example Usage:
```python
from website import Website

url = "https://example.com"
crawler = Website(url)
content = crawler.text
print(content)
```

### 2. Calling OpenAI API for Summarization
Function `summarize` calls OpenAI API for summarization

#### Code snippet:
```python
def summarize(url):
    website = Website(url)
    response = openai.chat.completions.create(
        model = "gpt-4o-mini",
        messages = messages_for(website)
    )
    return response.choices[0].message.content
```

## 🌟 Extended Features

### 1. Summarization with Ollama
This version of the summarization program replaces the OpenAI API with [Ollama](https://ollama.com/), an open-source alternative for running LLMs locally. It allows users to summarize text without external API calls, making it more cost-effective and private.

**Features:**
- Uses an on-device LLM through Ollama
- Summarizes large text inputs efficiently
- No API key required, runs entirely offline

**Requirements:**
- Install Ollama: Follow the instructions at [Ollama's official site](https://ollama.com/)
- Ensure the required model is downloaded

---

### 2. PowerPoint Slides Summarization
This feature enables users to summarize `.pptx` presentations using `python-pptx`. It extracts text from slides and generates a summary based on the extracted content.

**Features:**
- Parses `.pptx` files to extract text from slides
- Summarizes the extracted text using an LLM
- Supports batch processing of multiple slides

**Requirements:**
- Install dependencies:
  ```bash
  pip install python-pptx
  ```

## 📌 Notes
- Ensure your OpenAI API key is set in `.env` or as an environment variable.
- If crawling fails, check ChromeDriver installation and permissions.

## 📬 Contact
For any issues, please raise an issue in the repository or contact the maintainer.

