# Automating Fine-tuning Dataset Creation using Multimodal Generative AI Models

Prompts used in the blog post, [Automating Fine-tuning Dataset Creation using Multimodal Generative AI Models](https://garystafford.medium.com/automating-fine-tuning-dataset-creation-using-multimodal-generative-ai-models-a438fb6675e6).

## Example 1: Female Model Images - Captions

Desired JSONL-format output

```json
{"image-ref": "s3://bucket/path/to/image001.png", "caption": "<prompt text>"}
{"image-ref": "s3://bucket/path/to/image002.png", "caption": "<prompt text>"}
{"image-ref": "s3://bucket/path/to/image003.png", "caption": "<prompt text>"}
```

Prompt

```text
You are an expert at writing succinct, factual, non-biased descriptions of images.
Describe the facial expressions and emotions shown in each image of the young woman.
Do not attempt to identify or name specific individuals in images.
The order is of images in the grid left to right, top to bottom.
Return a "caption" corresponding to each image.
Each "caption" must start with the phrase "SusanJones the women". For example, "SusanJones the women smiling warmly with her teeth showing"
Output JSONL format in the following format: {"image-ref": "s3://sagemaker-us-east-1-123456789012/titan_image_finetune_dataset_01/images/susanjones_01.jpg", "caption": "SusanJones the women smiling warmly with her teeth showing"}
Increment the numeric suffix of each "image-ref". For example, susanjones_01.jpg, susanjones_02.jpg, susanjones_03.jpg
Only output the JSONL data; do not include an additional output, preamble, explanation, or chain of thought.
```

## Example 2: Single Image - Description

```text
You are an expert at writing succinct, factual, non-biased descriptions of images.
Write a 1-2 sentence description of the image.
Do not use phrases like "the image shows" or "appears to be".
Just output the description; do not include additional output, preamble, explanation, or chain of thought.
```

## Example 3: Sport Car Images - Captions

```text
You are an expert at writing succinct, factual, non-biased captions for images.
Write a Python 3 script that will produce individual text files, one for each image, containing a caption of the associated image.
The order is of images in the grid left to right, top to bottom.
Captions should be 1-2 sentences in length for each image.
Do not use phrases like "the image shows" or "appears to be".
Increment the filename for each caption. For example, car_1.txt, car_2.txt, car_3.txt.
Just output the Python script; do not include additional output, preamble, explanation, or chain of thought.
```

## Example 4: Sports Car Images - Tags

```text
You are an expert at creating a list of consistent, accurate, and non-biased keywords to describe images.
Write a Python 3 script that will produce individual text files, one for each image, containing a comma-delimited list of keywords describing the associated image.
The order is of images in the grid left to right, top to bottom.
The comma-delimited list of keywords for each image should be between 10-20 keywords.
Increment the filename for each description. For example, car_1.txt, car_2.txt, car_3.txt.
Just output the Python script; do not include additional output, preamble, explanation, or chain of thought.
```

## Example 5: Sports Car Images - Captions with Bedrock

Desired format of output, where `zsrtcar the car` is the unique token for the subject.

```text
zsrtcar the car <description of image 1-2 sentences>.
```

Prompt

```text
You are an expert at writing succinct, factual, non-biased captions for images.
Write a Python 3 script that will use the Amazon Bedrock Messages API for Anthropic Claude 3.5 Sonnet and produce individual text files, one for each image in the "images" directory, containing a caption of the associated image.
Descriptions should be 1-2 sentence caption for each image.
Start all captions with "zsrtcar the car". For example, "zsrtcar the car driving on a curvy road with trees in the background. Red body color with black rims."
Do not use phrases like "the image shows" or "appears to be".
Do not mention product names.
The filename for each text file must be the same as the corresponding image, but with a .txt extension.
Place the text files in the "image_captions" directory.
Do not forget to import json and base64 into the script, output a success message after each text file is created, and catch any errors.
Just output the Python script; do not include additional output, preamble, explanation, or chain of thought.
```

## Example 6: Sport Car Images - Tags with Bedrock

Desired format of output, where `zsrtcar the car` is the unique token for the subject.

```text
zsrtcar the car, tag1, tag2, tag3, tag4, tagN
```

Prompt

```text
You are an expert at creating consistent, accurate, and non-biased tags to describe images.
Write a Python 3 script that will use the Amazon Bedrock Messages API to call Anthropic Claude 3.5 Sonnet and produce individual text files, one for each PNG or JPEG image in the "images" directory, containing a comma-delimited list of descriptive tags describing the associated image.
The comma-delimited list for each PNG or JPEG image should contain 10-20 tags.
Do not mention product names.
All tags must be lowercase.
Always start the comma-delimited list with the unique tag "zsrtcar the car". For example, "zsrtcar the car, metallic blue, sports car, high-performance, driving, winding road, blue skys, fields, blurred background"
Never end the list with a period. The tag for the color of the subject should be separate. For example, "light blue", "bright red", metallic green", "white".
The filename for each text file must be the same as the corresponding image, but with a .txt extension.
Place the text files in the "image_captions" directory.
Output a success message after each text file is created, and catch any errors.
Just output the Python script; do not include additional output, preamble, explanation, or chain of thought.
```
