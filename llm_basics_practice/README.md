# LLM Basics Practice

A simple chatbot notebook that uses the Hugging Face Inference API to chat with an open-source LLM.

## 1. Download the notebook and upload it to Kaggle

1. On GitHub, open `llm_basics_practice/llm_basics.ipynb`.
2. Click the **Download raw file** button (the download icon near the top-right of the file view) to save `llm_basics.ipynb` to your computer.
3. Go to [https://www.kaggle.com](https://www.kaggle.com) and sign in (create a free account if you don't have one).
4. In the left sidebar, click **Your work** → **Create** → **<> New Notebook**.
5. Inside the new notebook, go to **File** → **Import Notebook** and upload the `llm_basics.ipynb` file you just downloaded.
6. (Recommended) In the right-hand panel, under **Session options**, make sure **Internet** is turned **On** — the notebook needs internet access to call the Hugging Face API.

## 2. Use the notebook

### a. Get a Hugging Face API token

1. Sign in (or sign up) at [https://huggingface.co](https://huggingface.co).
2. Go to **Settings (on the left)** → **Access Tokens** → **+ Create New token**.
3. Select the **Fine-grained** token type.
4. Give the token a name, then under permissions expand the **Inference** section and check the ALL inference-related permissions (e.g. **Make calls to Inference Providers** and **Make calls to your Inference Endpoints**).
5. Click **Create token**.
6. Copy the token (it starts with `hf_...`). You won't be able to see it again.

### b. Fill in the configuration cell

Open the second cell of the notebook and fill in the values:

- **`API_KEY`** — paste your Hugging Face token (e.g. `"hf_abc123..."`).
- **`MODEL_NAME`** — the model you want to chat with. For example:

    ```python
    MODEL_NAME = "meta-llama/Llama-3.1-8B-Instruct"
    ```

    You can browse other text-generation models at [huggingface.co/models](https://huggingface.co/models). Note: some models (like Llama) require accepting a license on their model page before you can use them.

    **Note:** The models have to be text-generation models.

- **`SYSTEM_PROMPT`** — defines the assistant's behavior and persona. For example:
    ```python
    SYSTEM_PROMPT = """\
    You are a helpful, friendly, and concise AI assistant.
    Answer the user's questions clearly and accurately.
    """
    ```
- **`LLM_PROPERTIES`** — controls how the model generates text:
    - `max_tokens` — maximum number of tokens to generate per reply (e.g. `512`).
    - `temperature` — randomness, between `0` and `1`. Lower = more deterministic, higher = more creative.
    - `top_p` — nucleus sampling threshold (e.g. `0.9`).
    - Any other properties. Click [here](https://huggingface.co/blog/inference-endpoints-llm#2-test-the-llm-endpoint) for a comprehensive list.

### c. Run the chatbot

1. Run the first cell to import `InferenceClient`.
2. Run the configuration cell (the second one) after filling it in.
3. Run the third cell to start the chatbot. You'll see:
    ```
    Chatbot ready! Type 'quit' to exit.
    You:
    ```
4. Type a message and press Enter to chat with the model. The full conversation history is sent on each turn, so the assistant remembers earlier messages.
5. Type `quit` to exit the chat loop.

### Troubleshooting

- **401 / authentication error**: double-check your `API_KEY` and that the token has at least Read permissions.
- **403 / gated model**: visit the model's page on Hugging Face and accept its license, then retry.
- **Model not found**: confirm the `MODEL_NAME` exactly matches the repo ID on Hugging Face (case-sensitive).
- **No input prompt appears on Kaggle**: make sure you're running the cell interactively and that **Internet** is enabled in the session options.
