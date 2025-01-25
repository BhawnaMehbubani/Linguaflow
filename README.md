# **Linguaflow: Multilingual Translation API**


## **Table of Contents**

1. [Objective](#objective)  
2. [How It Works](#how-it-works)  
3. [Pipeline Workflow](#pipeline-workflow)  
4. [Tech Stack](#tech-stack)  
5. [Setup and Installation](#setup-and-installation)  
   - [Prerequisites](#prerequisites)  
   - [Steps](#steps)  
6. [API Documentation](#api-documentation)  
   - [Root Endpoint](#1-root-endpoint)  
   - [Translation Endpoint](#2-translation-endpoint)  
7. [Key Features](#key-features)  
8. [Future Enhancements](#future-enhancements)  
9. [Contributions](#contributions)  



## **Objective**

Linguaflow is designed to provide seamless, high-performance multilingual translation capabilities using **FastAPI** and **Hugging Face's MarianMT** models. It enables developers to easily translate English text into multiple target languages, including **French**, **Portuguese**, and **Spanish**, with scalability and accuracy at its core.



## **How It Works**

The translation pipeline is straightforward yet powerful:

```
| Client Request | --> | FastAPI Endpoint (/translate) | --> | MarianMT Tokenizer | --> 
| MarianMT Model (Generate Translation) | --> | Decode Translations | --> | Response to Client |
```



## **Pipeline Workflow**

Below is a step-by-step workflow of the Linguaflow system:

```
1. Client Request:
   |-- A user sends a JSON payload to the `/translate` endpoint.
   |-- Example payload: {"src_text": [">>fra<< This is a test sentence."]}

2. Input Validation:
   |-- FastAPI validates the request payload using Pydantic's `BaseModel`.
   |-- Ensures the input follows the required schema.

3. Tokenization:
   |-- The MarianTokenizer from Hugging Face processes the input text.
   |-- Converts the text into token IDs compatible with the MarianMT model.
   |-- Adds any necessary padding for batch processing.

4. Translation:
   |-- The MarianMT model generates the translation in the specified target language.
   |-- Utilizes the Transformer architecture's encoder-decoder mechanism for efficient and accurate results.

5. Decoding:
   |-- The tokenized output from the model is decoded back into human-readable text.
   |-- Special tokens are removed to produce clean translations.

6. Response:
   |-- The translated text is encapsulated in a JSON response.
   |-- Example response: {"translated_text": ["Ceci est une phrase de test."]}
```



## **Tech Stack**

| **Component**       | **Technology**                  | **Description**                                                                 |
|----------------------|----------------------------------|---------------------------------------------------------------------------------|
| **Backend Framework**| FastAPI                         | High-performance framework for building APIs with Python.                      |
| **Translation Model**| MarianMT (Hugging Face)         | Pre-trained transformer models optimized for multilingual translation.         |
| **Data Validation**  | Pydantic                        | Ensures request payloads adhere to the expected schema.                        |
| **Server**           | Uvicorn                         | Lightning-fast ASGI server for running FastAPI apps.                           |
| **Libraries**        | Transformers, PyTorch           | Core libraries for loading and fine-tuning transformer models.                 |



## **Setup and Installation**

### **Prerequisites**
- **Python Version:** 3.8 or higher.
- **Package Manager:** pip (or Conda for virtual environments).

### **Steps**

#### 1. Clone the Repository
```bash
git clone <repository-url>
cd linguaflow
```

#### 2. Create a Virtual Environment
```bash
# On Windows
python -m venv venv
.\venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

#### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

#### 4. Run the Application
```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### 5. Test the API
Navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000) to access the root endpoint. Test the `/translate` endpoint using tools like **Postman**, **cURL**, or **Swagger UI** (automatically available via FastAPI).



## **API Documentation**

### **1. Root Endpoint**
- **URL:** `/`
- **Method:** `GET`
- **Description:** Confirms that the API is running.
- **Sample Response:**
  ```json
  {
    "message": "Welcome to the MarianMT Translation API!"
  }
  ```

### **2. Translation Endpoint**
- **URL:** `/translate`
- **Method:** `POST`
- **Description:** Translates English text into a target language.
- **Request Payload:**
  ```json
  {
    "src_text": [">>fra<< This is a test sentence to translate to French."]
  }
  ```
  - **Language Prefixes:**
    - `>>fra<<`: French
    - `>>por<<`: Portuguese
    - `>>spa<<`: Spanish

- **Response:**
  ```json
  {
    "translated_text": ["Ceci est une phrase de test à traduire en français."]
  }
  ```



## **Key Features**

1. **Multilingual Translation:**
   - Supports English to French, Portuguese, and Spanish translations.
   - Easily extensible to other languages supported by MarianMT.

2. **Asynchronous Processing:**
   - Handles concurrent requests efficiently, making it ideal for production-grade applications.

3. **User-Friendly Testing:**
   - Swagger UI and JSON responses simplify API integration and debugging.

4. **Error Handling:**
   - Built-in mechanisms for handling invalid inputs and unexpected exceptions.



## **Future Enhancements**

1. **Support for Additional Languages:**
   - Expand the API to include languages like German, Chinese, and Hindi.

2. **Advanced Features:**
   - Context-based translation to preserve tone and sentiment.
   - Batch processing for large-scale translation tasks.

3. **Deployment to Cloud:**
   - Deploy on AWS or Google Cloud for global scalability.



## **Contributions**

Contributions are welcome! Feel free to fork the repository, make improvements, and submit a pull request.
