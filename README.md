Extraction Pipeline:
This section will include the steps involved in the image processing and extraction pipeline.
Extraction Pipeline: The pipeline is designed to extract structured information from scanned handwritten medical prescriptions using a multimodal LLM.
Steps in the Pipeline:
Image Preprocessing:
The input images (medical prescriptions) are first loaded using the PIL library. This is done by reading the image from the file system, ensuring that it is in the right format for the model to process.
Model Initialization:
The Google Gemini model is initialized using the API key (stored in GEMINI_API_KEY). The model is configured to generate content based on the prompt provided.
Text Extraction:
The model is fed an OCR-based prompt that instructs it to extract structured data from the images. The fields extracted include:
Patient Name
Diagnosis
Test Results
Date of Examination
Doctor's Name
If any of these fields are not found in the image, the model outputs "Not Found" for the respective field.
Retries and Error Handling:
The function extract_plain_text_with_retry incorporates a retry mechanism to handle API rate limits (error 429). If the model exceeds the rate limit, it waits for a specified delay before retrying the extraction (up to 3 retries).
Parsing the Model Response:
The model response, which contains the extracted information, is returned as raw text. The raw text is parsed using a regular expression to extract the structured JSON data.
Data Storage:
The extracted data is stored in a list (all_data). Each data point includes the extracted information, along with the filename for reference.
After processing all images, the list is converted into a Pandas DataFrame and saved into an Excel file for further analysis and use.
Output:
The resulting DataFrame is saved as an Excel file to the specified path (output_excel_path), providing a structured output for analysis.


Here's how the multimodal model is used:
Model Setup: We use the Gemini 1.5 Pro model to process the images. The model is called via the google.generativeai library, and it is configured using the API key.
Prompting the Model: The key aspect of utilizing this model lies in the prompt that we provide. We define the required fields (Patient Name, Diagnosis, Test Results, etc.) in the prompt, instructing the model to extract these fields from the provided image. The model generates a structured response in JSON format containing the extracted information.
Text Processing: The model processes the image in the form of text prompts, converting the image’s content into structured data. This involves identifying and extracting specific fields (like diagnosis, doctor’s name, etc.) from the text that appears in the image. The model is built to handle text extraction from scanned handwritten documents, which is crucial in medical prescriptions.

Evaluation strategy:
Since there is no labeled dataset for ground truth, the model’s performance is evaluated manually. The extracted data is reviewed and compared to the actual content of the handwritten prescriptions to ensure accuracy.

Future Evaluation (With Labeled Data):
If labeled data becomes available, cosine similarity can be used to compare the generated text with the reference text. Cosine similarity measures how closely the two texts match, providing an objective metric for evaluation
