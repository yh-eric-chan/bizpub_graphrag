# Tutorial: Implementing GraphRAG and Adapting It to a Domain-Specific Task

## App Website: 
[BizPub GraphRAG](https://huggingface.co/spaces/ericyhchen/bizpub_graphrag)

## Our Workflow:

<img width="468" alt="image" src="https://github.com/user-attachments/assets/5d2c9800-5344-4b20-bc52-a9a5ac0d3120">

## Dataset

We assembled a dataset comprising abstracts from all UTD24 and FT50 journal articles published since January 2024. This dataset contains 2,714 papers from 52 journals, covering six major business disciplines, as illustrated in Figure 2.

<img width="404" alt="image" src="https://github.com/user-attachments/assets/c2e0838d-10c2-42cc-84e2-b7554ecc53e1">


---

## Prerequisites

Ensure you have a Python environment set up with the required dependencies. You can install GraphRAG via `pip`.

### Step 1: Install the GraphRAG Package

Install GraphRAG using the following command:

```bash
pip install graphrag
```

### Step 2: Initialize GraphRAG

Once installed, initialize the GraphRAG environment:

```bash
python -m graphrag.index --init --root ./ragt
```

### Step 3: Create Input Directory and Add Your Data

Create an input directory for your documents and place your data inside:

```bash
mkdir -p ./ragtest/input
```

### Step 4: Configure API and Settings

Add the necessary API keys in your environment and configure the `settings.yaml` file. Make sure the configuration is appropriate for your task. Use the `4omini` configuration as a baseline and adjust parameters as needed.

### Step 5: Index the Raw Data

Index your raw data using GraphRAG with the following command:

```bash
python -m graphrag.index --root ./ragtest
```

### Step 6: Perform Prompt Tuning

Now, you can adjust the prompts according to your domain (in this case, "business research paper"). Use the command below to run prompt tuning:

```bash
python -m graphrag.prompt_tune --root ./ragtest --config /Users/yihong_eric_chen/24S_Research/graphrag/ragtest/settings.yaml --domain "business research paper" \
--selection-method random --limit 10 --language English --max-tokens 2048 --chunk-size 256 --min-examples-required 3 \
--no-entity-types --output ./ragtest/modified_prompt
```

### Step 7: Modify the `settings.yaml` File for Prompt Adjustment

Remember to adjust the relevant sections of the `settings.yaml` file for prompt-specific tuning in this step. This is crucial for adapting the model to your domain-specific task.

### Step 8: Implement the Hybrid Prompt Tuning to Further Improve Auto-Tuned Prompt

Raw Prompt vs Auto-tuned Prompt vs Hybrid Prompt

<img width="468" alt="image" src="https://github.com/user-attachments/assets/6438fc70-b2cc-4834-9e09-579c8e5e0e44">
