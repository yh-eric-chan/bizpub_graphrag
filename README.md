# Tutorial: Implementing GraphRAG and Adapting It to a Domain-Specific Task

## App Website and Demo:
- [BizPub GraphRAG](https://huggingface.co/spaces/ericyhchen/bizpub_graphrag)
- [Video Demo](https://www.loom.com/share/5ebdae83932f4dc797e8ab5b2e510739?sid=dbdea7f2-a35c-4b51-8d4f-741c36241c97)

---

## Workflow Overview

This tutorial guides you through implementing GraphRAG and adapting it to a domain-specific task using business research papers as an example.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/5d2c9800-5344-4b20-bc52-a9a5ac0d3120">

---

## Dataset

We assembled a dataset comprising abstracts from all UTD24 and FT50 journal articles published since January 2024. This dataset includes 2,714 papers from 52 journals, covering six major business disciplines, as shown below:

<img width="600" alt="image" src="https://github.com/user-attachments/assets/c2e0838d-10c2-42cc-84e2-b7554ecc53e1">

---

## Prerequisites

Before proceeding, ensure your Python environment is set up with the required dependencies. GraphRAG can be installed via `pip`.

---

## Steps to Implement GraphRAG

### Step 1: Install the GraphRAG Package

Use the following command to install GraphRAG:

```bash
pip install graphrag
```

### Step 2: Initialize GraphRAG

After installation, initialize GraphRAG with the following command:

```bash
python -m graphrag.index --init --root ./ragt
```

### Step 3: Create Input Directory and Add Your Data

Create a directory to store your input documents:

```bash
mkdir -p ./ragtest/input
```

Place your data (e.g., business research abstracts) inside the `input` directory.

### Step 4: Configure API and Settings

Add the necessary API keys to your environment and configure the `settings.yaml` file. Ensure that the configuration matches your requirements. For optimal cost efficiency, it’s recommended to use the `gpt-4o-mini` model in your configuration:

```yaml
model: gpt-4o-mini
```

You may want to create an `.environment` file to securely store your `GRAPHRAG_API_KEY`.

### Step 5: Index the Raw Data

Run the following command to index your raw data using GraphRAG:

```bash
python -m graphrag.index --root ./ragtest
```

### Step 6: Perform Prompt Tuning

To tailor the model’s prompts for your domain (in this case, "business research paper"), use the following command:

```bash
python -m graphrag.prompt_tune --root ./ragtest --config /Users/yihong_eric_chen/24S_Research/graphrag/ragtest/settings.yaml --domain "business research paper" \
--selection-method random --limit 10 --language English --max-tokens 2048 --chunk-size 256 --min-examples-required 3 \
--no-entity-types --output ./ragtest/modified_prompt
```

### Step 7: Modify the `settings.yaml` for Prompt Adjustment

In this step, adjust the `settings.yaml` file to fine-tune prompts for your task. Update the path for the prompt file:

```yaml
prompt: "{YOUR PATH TO THE PROMPTS}/summarize_descriptions.txt"
```

This modification is essential for aligning the model to your specific domain requirements.

### Step 8: Implement Hybrid Prompt Tuning for Improved Results

To further enhance the prompt performance, use a hybrid approach combining raw and auto-tuned prompts. Compare raw, auto-tuned, and hybrid prompts to refine your results.

For detailed insights, refer to the comparison below:

<img width="600" alt="image" src="https://github.com/user-attachments/assets/6438fc70-b2cc-4834-9e09-579c8e5e0e44">


