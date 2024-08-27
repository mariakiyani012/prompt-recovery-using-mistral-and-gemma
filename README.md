# LLM Prompt Recovery
## Overview
This project aims to recover the prompts used to transform original text into rewritten text using large language models (LLMs). It utilizes models from the Hugging Face Transformers library and integrates various techniques for text transformation and generation.

## Features
Text Transformation: Recover prompts used for transforming original text into rewritten text.
Model Support: Compatible with different LLMs including Gemma and Mistral.
Quantization Support: Option to use 4-bit quantization for reduced model size and faster inference.
Custom Prompts: Ability to specify custom prompts and transformation instructions.

## Installation
First, ensure you have the necessary dependencies installed:

`
pip install ../input/hf-peft/peft-0.9.0-py3-none-any.whl
`

`
pip install ../input/bitsandbytes/bitsandbytes-0.42.0-py3-none-any.whl
`

`
pip install ../input/transformers-4-39-2/transformers-4.39.2-py3-none-any.whl
`

## Usage
Prepare Your Environment

Ensure you have a CSV file (test.csv) with original_text and rewritten_text columns for testing.

Run the Script

Execute the script with the desired parameters. Here is an example command:

`
python run.py --model_path /path/to/model --peft_path /path/to/peft --model_type "mistral" --output "predictions.json" --max_len 512 --test_path ./test.csv --quantize --prime "It's likely that the prompt that transformed original_text to new_text was: Rewrite" --magic ""
`

Replace the placeholders with appropriate paths and parameters:

--model_path: Path to the pre-trained model.
--peft_path: Path to the PEFT model, if applicable.
--model_type: Type of model to use (gemma or mistral).
--output: File path to save predictions.
--max_len: Maximum length of input text.
--test_path: Path to the CSV file with test data.
--quantize: Flag to enable 4-bit quantization.
--prime: Custom prompt for generating text.
--magic: Placeholder text for predictions.


## Combine Predictions

After running the script, combine the predictions from multiple models if needed:
fns = ["pred0.json", "pred1.json"]
preds = [json.load(open(x)) for x in fns]
preds = [' '.join(list(x)) for x in zip(*preds)]
print(preds[:2])

## Code Description
run.py: Main script for loading models, running predictions, and saving results.
predict_gemma: Function for predicting with the Gemma model.
predict_mistral: Function for predicting with the Mistral model.


## License
This project is licensed under the MIT License. See the LICENSE file for details.
