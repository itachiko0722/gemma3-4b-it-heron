# gemma3-4b-it-herron

## Overview

- **Model:** Gemma 3 instruction-tuned ([google/gemma-3-4b-it](https://huggingface.co/google/gemma-3-4b-it))
- **Questions:** `questions_ja.jsonl`, a JSON Lines file containing questions with fields such as `question_id`, `image`, `context`, and the main text of the question.
- **Images:** Stored locally in the same directory as the script, referenced by filename in `questions_ja.jsonl` (e.g., `"001.jpg"`).

The script loads Gemma 3 from Hugging Face, processes each question and the corresponding local image, and outputs answers to `gemma3_output.jsonl`.

## File Structure

```
.
├─ questions_ja.jsonl       # Input question file (JSON Lines)
├─ 001.jpg                  # Example local images
├─ 002.jpg
├─ 003.jpg
├─ gemma_heron_eval.py      # Main Python script
└─ gemma3_output.jsonl      # Output file with generated answers
```

## Environment Setup

### 1. Install Python

Python 3.8 or higher is recommended.

### 2. Create a Virtual Environment (recommended)

```bash
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
```

### 3. Install Required Libraries

```bash
pip install torch transformers
```

Ensure you have `transformers >= 4.50.0`. CUDA is optional but recommended for faster processing.

### 4. Hugging Face Authentication (Optional)

If the model requires authentication:

```bash
huggingface-cli login
```

## Output File (gemma3_interface-heron.jsonl)

Each line is a valid JSON object:

```json
{
  "question_id": 0,
  "image": "001.jpg",
  "category": "complex",
  "image_category": "anime",
  "context": "Additional context about the scene.",
  "text": "What is happening in this image?"
}
```

- **question\_id:** Unique ID for each question.
- **image:** Local filename (e.g., `"001.jpg"`).
- **category/image\_category:** Optional labels.
- **context:** Additional context or prompt.
- **text:** The question in Japanese.

## Script Explanation

`gemma_heron_eval.py` performs the following:

- Loads Gemma 3 model and processor.
- Reads `questions_ja.jsonl` line-by-line.
- Creates chat-style inputs for Gemma 3.
- Generates and saves answers to `gemma3_output.jsonl`.

## Important Notes

- **Local Images:** Ensure images are correctly placed relative to the script.
- **Authentication:** Use Hugging Face CLI login if required.
- **Device Mapping:** `device_map="auto"` utilizes GPU if available; CPU-only inference is possible but slower.

## License

- Gemma 3 by Google DeepMind available on Hugging Face.
- Japanese-Heron-Bench evaluates Japanese VLM performance.

Please refer to respective licenses for usage terms.


