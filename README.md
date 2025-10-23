# Image Similarity Search with Azure AI Vision and PostgreSQL

This project demonstrates a simplified image similarity search application using Azure AI Vision for generating embeddings and Azure Database for PostgreSQL Flexible Server as a vector database. This is an adapted version focusing on the core functionality of vector search.

## Special Thanks

Special thanks to **[Foteini Savvidou](https://github.com/sfoteini)** for the original [vector-search-azure-cosmos-db-postgresql](https://github.com/sfoteini/vector-search-azure-cosmos-db-postgresql) repository. This project uses and adapts parts of her code to create a simplified version for learning and demonstration purposes.

## Overview

This application enables you to search for similar paintings using either text prompts or reference images. The project utilizes:

- **Azure AI Vision**: Multi-modal embeddings API for generating vector embeddings from images and text
- **Azure Database for PostgreSQL Flexible Server**: Vector database with pgvector extension for similarity search
- **SemArt Dataset**: A collection of approximately 21k paintings from the Web Gallery of Art

## Prerequisites

Before you start, ensure you have the following:

- **Azure Subscription** - Create an [Azure free account](https://azure.microsoft.com/free/) or [Azure for Students account](https://azure.microsoft.com/free/students/)
- **Azure AI Foundry Project** - With an Azure AI Vision connection configured
- **Azure Database for PostgreSQL Flexible Server** - [Create a server](https://learn.microsoft.com/azure/postgresql/flexible-server/quickstart-create-server-portal) and [enable the pgvector extension](https://learn.microsoft.com/azure/postgresql/flexible-server/how-to-use-pgvector)
- **Python 3.10+** and Visual Studio Code with Jupyter extension

> **Note**: Azure AI Vision multi-modal embeddings APIs are available in: East US, France Central, Korea Central, North Europe, Southeast Asia, West Europe, West US.

## Setup

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd se_data_ai_image_embedding_example
```

### 2. Download the Dataset

Download the [SemArt Dataset](https://researchdata.aston.ac.uk/id/eprint/380/) and extract it into the `semart_dataset` directory.

### 3. Install Dependencies

This project uses [uv](https://docs.astral.sh/uv/) for fast Python package management. If you don't have uv installed, install it first:

```bash
# On Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# On macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Create a virtual environment and install dependencies:

```bash
# Sync dependencies from uv.lock (recommended - ensures exact versions)
uv sync

# Activate the virtual environment
# On Windows
.venv\Scripts\activate
# On macOS/Linux
source .venv/bin/activate
```

Alternatively, if you don't have a `uv.lock` file:

```bash
# Create virtual environment and install from requirements.txt
uv venv
uv pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Azure AI Foundry Project
PROJECT_ENDPOINT=<your-ai-foundry-project-endpoint>

# Azure Database for PostgreSQL Flexible Server
POSTGRES_HOST=<your-postgres-host>
POSTGRES_DB_NAME=<your-database-name>
POSTGRES_USER=<your-username>
POSTGRES_PASSWORD=<your-password>
POSTGRES_TABLE_NAME=<your-table-name>

# Azure AI Vision
VISION_VERSION=?api-version=2024-02-01&model-version=2023-04-15
```

## Project Structure

```
se_data_ai_image_embedding_example/
├── notebooks/
│   ├── data_preprocessing.ipynb      # Clean and prepare the SemArt dataset
│   ├── generate_embeddings.ipynb     # Generate embeddings using Azure AI Vision
│   └── image_search.ipynb            # Image similarity search demonstrations
├── modules/
│   ├── constants.py                  # Constants and configuration
│   └── utils.py                      # Utility functions
├── dataset/                          # Processed dataset files
├── semart_dataset/                   # Original SemArt dataset
│   └── Images/                       # Dataset images
├── .env                              # Environment variables (create this)
└── README.md
```

## How to Use

### Step 1: Data Preprocessing

Run the `notebooks/data_preprocessing.ipynb` notebook to clean up the SemArt Dataset and create the final dataset.

### Step 2: Generate Embeddings

Run the `notebooks/generate_embeddings.ipynb` notebook to:
- Connect to Azure AI Foundry project
- Retrieve Azure AI Vision connection
- Generate vector embeddings for images
- Save embeddings to `dataset/dataset_embeddings.csv`

### Step 3: Upload Data to PostgreSQL

Use the provided scripts or notebooks to:
- Create a table in Azure Database for PostgreSQL Flexible Server
- Populate it with image metadata and embeddings
- Enable vector similarity search with pgvector

### Step 4: Image Search

Run the `notebooks/image_search.ipynb` notebook to explore:

- **Text-to-Image Search**: Find images similar to a text description
- **Image-to-Image Search**: Find images similar to a reference image
- **Metadata Filtering**: Combine vector search with SQL filters
- **Cosine Similarity**: Calculate and display similarity scores

## Key Features

- **Azure AI Foundry Integration**: Seamlessly connect to Azure AI Vision through Azure AI Foundry projects
- **Local Image Loading**: Images are loaded directly from the local filesystem for faster development
- **Simplified Workflow**: Focused on core vector search functionality
- **Interactive Notebooks**: Step-by-step guidance through Jupyter notebooks

## Example Use Cases

1. **Search by Description**: "a table with flowers"
2. **Search by Artist**: Filter paintings by specific artists (e.g., Vincent van Gogh)
3. **Search by Reference Image**: Upload an image and find similar paintings
4. **Similarity Scoring**: View cosine similarity scores for search results

## Resources

### Azure Documentation

- [Azure AI Vision Multi-modal Embeddings](https://learn.microsoft.com/azure/ai-services/computer-vision/concept-image-retrieval)
- [How to Use pgvector on Azure Database for PostgreSQL Flexible Server](https://learn.microsoft.com/azure/postgresql/flexible-server/how-to-use-pgvector)
- [Azure AI Foundry Projects](https://learn.microsoft.com/azure/ai-studio/)

### Related Blog Posts by Foteini Savvidou

- [Use the Azure AI Vision multi-modal embeddings API for image retrieval](https://sfoteini.github.io/blog/azure-ai-vision-multimodal-embeddings-api/)
- [Generate embeddings with Azure AI Vision multi-modal embeddings API](https://sfoteini.github.io/blog/azure-ai-vision-multimodal-embeddings-generate/)
- [Store embeddings in Azure Cosmos DB for PostgreSQL with pgvector](https://sfoteini.github.io/blog/azure-cosmos-db-postgresql-pgvector-store-embeddings/)
- [Use pgvector for searching images on Azure Cosmos DB for PostgreSQL](https://sfoteini.github.io/blog/azure-cosmos-db-postgresql-pgvector-image-search/)

### Additional Resources

- [pgvector GitHub Repository](https://github.com/pgvector/pgvector)
- [SemArt Dataset](https://researchdata.aston.ac.uk/id/eprint/380/)

## License

This project adapts code from the original [vector-search-azure-cosmos-db-postgresql](https://github.com/sfoteini/vector-search-azure-cosmos-db-postgresql) repository by Foteini Savvidou.

## Contributing

Feel free to experiment with the project and modify the code to meet your specific use cases and requirements!
