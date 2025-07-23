# AI Unleashed Demo - Azure AI Search Implementation

This repository contains a comprehensive demonstration of Azure AI Search capabilities using various document processing techniques including OCR and layout analysis. The notebooks showcase end-to-end implementation of intelligent document search with vector embeddings and Azure OpenAI integration.

## 📋 Prerequisites

- Azure subscription with the following services (place in same region):
  - Azure AI Search
  - Azure Blob Storage
  - Azure OpenAI Service
  - Azure AI Services (for OCR and layout analysis)
- Python 3.8+
- Jupyter environment or VS Code with Python extension

- For custom embedding model: https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/custom-vectorizer/readme.md

## AI Search Pre-req:
-Set Semantic Ranker Enablement

## Pre-req permissions
- Set to use Manged Indentities:
  - Use Managed Identiy on Azure OpenAI
    - Identity -> System Assigned Set to "On"

  - Use Managed Identity on AI Search
    - Identity -> System Assigned Set to "On"
    - Settings > Keys > Select Role-based access control or Both

- Set Permisions:

On AI Search Assign Search Service Contributor to yourself & managed id connecting
On AI Search Assign Search Index Data Contributor to yourself & maanged id connecting
On Blob Storage Assign Blob Data Contirbutor 



## 🚀 Getting Started

### 1. Environment Setup

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd ai-unleashed-demo
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure environment variables:
   - Copy `.env.sample` to `.env`
   - Fill in your Azure service credentials and endpoints

### 2. Environment Variables

The following environment variables are required (see `.env.sample` for template):

- **Azure Search**: Service name, endpoint, API key, and index names
- **Azure Blob Storage**: Connection string and container name
- **Azure OpenAI**: Endpoint, API key, and model configurations
- **Azure AI Services**: Endpoint for cognitive services

## 📚 Notebook Overview

### 000_CreateIndex.ipynb
**Purpose**: Foundation setup for Azure AI Search infrastructure

**What it does**:
- Creates Azure AI Search data sources
- Defines search index schema with vector fields
- Sets up semantic search configuration
- Configures skillsets for document processing
- Creates and runs indexers

**Key Features**:
- Vector search with Azure OpenAI embeddings
- Semantic search capabilities
- Document chunking and processing pipeline

### 001 UseOCRForPageNumbers.ipynb
**Purpose**: OCR-based document processing with page number extraction

**What it does**:
- Implements OCR (Optical Character Recognition) for document text extraction
- Extracts page numbers from documents
- Creates specialized index for OCR-processed content
- Generates embeddings for searchable text chunks

**Key Features**:
- OCR skill integration
- Page-level document processing
- Text chunking with overlap
- Vector embedding generation

**Use Case**: Best for scanned documents, PDFs with images, or documents where page-level granularity is important.

### 001 UseOCRForPageNumbers copy.ipynb
**Purpose**: Duplicate/variation of the OCR implementation

**What it does**:
- Similar functionality to the original OCR notebook
- May contain experimental variations or backup implementation
- Demonstrates OCR-based indexing approach

### 002 UseLayoutForDocument.ipynb
**Purpose**: Layout analysis for structured document processing

**What it does**:
- Uses Azure AI Document Intelligence for layout analysis
- Extracts structured information (tables, forms, key-value pairs)
- Processes documents with complex layouts
- Creates layout-aware search index

**Key Features**:
- Document layout analysis
- Table and form extraction
- Structured data processing
- Layout-aware chunking

**Use Case**: Ideal for structured documents like forms, reports, invoices, or documents with complex layouts.

### 003 Azure OpenAI.ipynb
**Purpose**: Azure OpenAI integration and chat functionality

**What it does**:
- Demonstrates Azure OpenAI API integration
- Shows chat completions with and without data sources
- Implements retrieval-augmented generation (RAG)
- Tests embedding generation

**Key Features**:
- Chat completions API usage
- RAG implementation with Azure AI Search
- Embedding model integration
- Authentication methods (API key and managed identity)

**Use Case**: Building conversational AI applications that can query your indexed documents.

## 🔧 Technical Architecture

### Data Flow
1. **Document Upload** → Azure Blob Storage
2. **Processing Pipeline** → Azure AI Search Indexer
3. **Cognitive Skills** → OCR/Layout Analysis + Text Splitting
4. **Embedding Generation** → Azure OpenAI
5. **Index Storage** → Azure AI Search
6. **Query Processing** → Vector + Semantic Search
7. **Response Generation** → Azure OpenAI Chat

### Index Structure
Each notebook creates indexes with the following common fields:
- `parent_id`: Document identifier
- `title`: Document title/name
- `chunk_id`: Unique chunk identifier (primary key)
- `chunk`: Text content
- `vector`: Embedding vector for similarity search
- `page_number`: Page reference (OCR-specific)

## 📖 Usage Patterns

### For OCR Processing (Notebooks 001)
Best for:
- Scanned documents
- Image-heavy PDFs
- Documents requiring page-level search
- Legacy document digitization

### For Layout Analysis (Notebook 002)
Best for:
- Forms and structured documents
- Reports with tables and charts
- Invoices and receipts
- Documents with complex formatting

### For Chat Integration (Notebook 003)
Best for:
- Building Q&A systems
- Conversational document search
- Customer support applications
- Knowledge base interactions

## 🔍 Search Capabilities

The implementation supports multiple search modes:
- **Vector Search**: Semantic similarity using embeddings
- **Hybrid Search**: Combines vector and keyword search
- **Semantic Search**: Azure's semantic ranking
- **Filtered Search**: Based on metadata and page numbers

## 🛠️ Customization

### Modifying Skillsets
Each notebook includes skillset definitions that can be customized:
- Adjust chunking parameters (`maximumPageLength`, `pageOverlapLength`)
- Modify OCR settings (`detectOrientation`, `lineEnding`)
- Configure embedding dimensions and models

### Index Schema
Customize the index schema to include additional fields:
- Document metadata
- Custom categories
- Date fields
- Numerical fields for filtering

## 🚨 Important Notes

1. **Security**: Never commit your `.env` file with real credentials
2. **Costs**: Monitor Azure service usage, especially for large document sets
3. **Limits**: Be aware of Azure AI Search and OpenAI service limits
4. **Performance**: Consider batch processing for large document collections

## 🔗 Additional Resources

- [Azure AI Search Documentation](https://docs.microsoft.com/azure/search/)
- [Azure OpenAI Service Documentation](https://docs.microsoft.com/azure/cognitive-services/openai/)
- [Azure AI Document Intelligence](https://docs.microsoft.com/azure/applied-ai-services/form-recognizer/)

## 🤝 Contributing

Feel free to contribute improvements, bug fixes, or additional examples. Please ensure all sensitive information is removed before submitting pull requests.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
