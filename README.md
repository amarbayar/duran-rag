# ID-based RAG FastAPI

## Overview
This project integrates Langchain with FastAPI in an Asynchronous, Scalable manner, providing a framework for document indexing and retrieval, using PostgreSQL/pgvector.

Files are organized into embeddings by `file_id`. The primary use case is for integration with [LibreChat](https://librechat.ai), but this simple API can be used for any ID-based use case.

The main reason to use the ID approach is to work with embeddings on a file-level. This makes for targeted queries when combined with file metadata stored in a database, such as is done by LibreChat.

The API will evolve over time to employ different querying/re-ranking methods, embedding models, and vector stores.

## Features
- **Document Management**: Methods for adding, retrieving, and deleting documents.
- **Vector Store**: Utilizes Langchain's vector store for efficient document retrieval.
- **Asynchronous Support**: Offers async operations for enhanced performance.
- **JWT Auth**: Set a `JWT_SECRET` to require authenticated requests.

## Setup

### Getting Started

- **Configure `.env` file based on [section below](#environment-variables)**
- **Setup pgvector database:**
  - Run an existing setup, or,
  - Use main `docker-compose.yaml`: `docker compose up`
- **Run API**:
  - Use Docker:
    - With PgVector: `docker compose -f ./db-api-compose.yaml up`
    - Without: `docker compose -f ./api-compose.yaml up`
  - Install locally:
```bash
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000
```

### Environment Variables

The following environment variables are required to run the application:

- `OPENAI_API_KEY`: The API key for OpenAI API Embeddings.
- `POSTGRES_DB`: The name of the PostgreSQL database.
- `POSTGRES_USER`: The username for connecting to the PostgreSQL database.
- `POSTGRES_PASSWORD`: The password for connecting to the PostgreSQL database.
- `DB_HOST`: The hostname or IP address of the PostgreSQL database server.
- `DB_PORT`: The port number of the PostgreSQL database server.

- `JWT_SECRET`: (Optional) The secret key used for verifying JWT tokens for requests.
  - The secret is only used for verification. This basic approach assumes a signed JWT from elsewhere.
  - Omit to run API without requiring authentication

- `COLLECTION_NAME`: (Optional) The name of the collection in the vector store. Default value is "testcollection".
- `CHUNK_SIZE`: (Optional) The size of the chunks for text processing. Default value is "1500".
- `CHUNK_OVERLAP`: (Optional) The overlap between chunks during text processing. Default value is "100".
<!-- - `UPLOAD_DIR`: (Optional) The directory where uploaded files are stored. Default value is "./uploads/". -->
- `PDF_EXTRACT_IMAGES`: (Optional) A boolean value indicating whether to extract images from PDF files. Default value is "False".
- `DEBUG_RAG_API`: (Optional) Set to "True" to show more verbose logging output in the server console, and to enable postgresql database routes

Make sure to set these environment variables before running the application. You can set them in a `.env` file or as system environment variables.

