# DeepSeek Demo In Jupyter Notebook

This repository provides a Jupyter Notebook environment for using the DeepSeek-AI model (and any other models available on Hugging Face) to generate code responses based on user prompts. It includes a GPU-accelerated setup and a CPU-only branch for local execution.

For a detailed walkthrough of this repository and its features, check out my video on my [YouTube channel](https://www.youtube.com/channel/UCc12pd-7Kyg73mU4cbW-mzg?sub_confirmation=1).

## Features
- Uses the **DeepSeek-Coder-1.3B-Instruct** model
- Supports both **GPU-accelerated** and **CPU-only** execution
- Provides a **Gradio-based UI** for interactive code generation
- Includes **VS Code DevContainer support** for easy reproducibility

## Setup Instructions
### 1. Clone the Repository
```sh
git clone https://github.com/Perpetue237/deepseek_demo.git
cd deepseek-demo
```

### 2. Setup Environment
Ensure you have a Hugging Face API token. Create a `.devcontainer/devcontainer.env` file and add:
```
HF_TOKEN=<your_huggingface_token>
```

### 3. Choose a Branch
#### GPU-Accelerated Setup (Default)
The default branch uses **PyTorch with CUDA** for GPU acceleration. This setup is defined in the following DevContainer:

```json
{
  "name": "DeepSeek Notebook",
  "image": "pytorch/pytorch:2.6.0-cuda12.6-cudnn9-devel",
  "postCreateCommand": "pip install jupyter ipykernel transformers accelerate sentencepiece gradio ipywidgets",
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "ms-toolsai.jupyter",
        "RSIP-Vision.nvidia-smi-plus"
      ]
    }
  },
  "runArgs": ["--env-file=.devcontainer/devcontainer.env", "--gpus", "all"],
  "mounts": [
    "source=${localWorkspaceFolder},target=/workspace,type=bind"
  ]
}
```
To use this version, simply **checkout the main branch** and open the folder in VS Code.

```sh
git checkout main
```

#### CPU-Only Setup (Local Execution)
If you don’t have a GPU, switch to the **CPU-only** branch, which uses a lighter DevContainer:

```sh
git checkout cpu-only
```

The CPU-only DevContainer is defined as follows:

```json
{
    "name": "DeepSeek local Demo",
    "image": "python:3.11-bullseye",
    "postCreateCommand": "pip install torch jupyter ipykernel transformers accelerate sentencepiece gradio ipywidgets",
    "runArgs": [
        "--env-file=.devcontainer/devcontainer.env"
    ],
    "customizations": {
        "vscode": {
            "extensions": [
                "RSIP-Vision.nvidia-smi-plus",
                "ms-python.python",
                "ms-toolsai.jupyter"
            ]
        }
    }
}
```

### 4. Start the Notebook
After setting up the environment, open the DevContainer in VS Code and start the Jupyter Notebook:

```sh
jupyter notebook
```

## Running the Model
The `deepseek_notebook.ipynb` file contains the necessary code to load the DeepSeek model and generate responses. Here’s a summary:

1. **Load the model**: The script automatically downloads the model (if not already saved) or loads it from disk.
2. **Generate responses**: Uses `transformers` to generate AI-powered code solutions.
3. **Gradio UI**: Provides an interactive chat interface for code generation.

Run the notebook cells to generate AI-assisted Python code snippets!

## Commit Guidelines
Since models are large, add the following to `.gitignore`:
```
models/
.gradio/
.env
```
Before pushing, ensure you don’t accidentally commit your Hugging Face token:
```sh
git add .
git commit -m "DeepSeek Demo with Gradio"
git push origin main
```

## Conclusion
This repository provides an environment for experimenting with DeepSeek-AI and any other models available on Hugging Face. You can use GPU acceleration for faster performance or switch to the CPU-only branch if you lack a compatible GPU.

Enjoy coding with DeepSeek-AI! 🚀