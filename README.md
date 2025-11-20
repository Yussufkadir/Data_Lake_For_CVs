# 🎯 Azure Data Lake - NER Data Pipeline
------------------------------------

## Overview
This project implements a medallion architecture data lake on Azure Data Lake Storage Gen2 for managing and processing Named Entity Recognition (NER) training data.
Architecture
Medallion Data Lake Pattern
The data lake follows the bronze-silver-gold architecture pattern:
```
cv-data-layers/
├── bronze/    # Raw, unprocessed data
├── silver/    # Cleaned and validated data
└── gold/      # Enriched, production-ready data
```
## Data Flow

**Bronze Layer** - Raw NER datasets with:

- Unstructured data formats
- Missing values and incomplete annotations
- Poorly formatted NER tags
- Original source data preserved as-is


**Silver Layer** - Cleaned data with:

- Standardized data formats
- Removed duplicates and null values
- Validated NER annotations
- Consistent structure ready for processing


**Gold Layer (Planned)** - Production-ready data:

- Fully annotated NER datasets
- Quality-validated entities
- Ready for model training
- Optimized for consumption



## 🛠️ Azure Infrastructure
### Services Used

- Azure Data Lake Storage Gen2 - Hierarchical namespace enabled for efficient data organization
- Storage Account: cvdatastoragetotest
- Region: Poland Central
- Container: cv-data-layers

## 🪄 Key Features

Hierarchical Namespace: Enabled for true data lake capabilities
### Security:

- HTTPS traffic only
- TLS 1.2 minimum
- Private blob access
- 7-day soft delete retention


**Performance**: Hot access tier for frequently accessed data
**Redundancy**: Locally Redundant Storage (LRS)

## 🔄 Setup Process
Manual Setup Steps
This data lake was built through the Azure Portal with the following steps:

Created Storage Account

**Resource type**: StorageV2 (general purpose v2)
Performance: Standard
Replication: LRS
Enabled hierarchical namespace for Data Lake Gen2


### Created Container

Name: cv-data-layers
Access level: Private


### Created Folder Structure

Bronze layer for raw data ingestion
Silver layer for cleaned data
Gold layer for production-ready datasets


### Uploaded Data

Raw NER training data uploaded to bronze layer
Cleaned datasets placed in silver layer
Manual upload through Azure Portal UI



## Why Azure ❓
After evaluating multiple cloud platforms, I chose Azure for this project because:

**Intuitive Interface** - Azure Portal's UI made it easier to understand data lake concepts and organize hierarchical data
**Student Accessibility** - Straightforward Azure for Students program with $100 credit, no credit card required
**Better Developer Experience** - Cleaner service organization compared to AWS's complex console
**Learning Focus** - Could concentrate on data lake architecture and NER data processing rather than platform complexity

## 📊 Data Processing
Current State

✅ Bronze layer: Raw NER data with quality issues ingested
✅ Silver layer: Data cleaning and validation completed
🔄 Gold layer: NER annotation in progress

## 🔜 Planned Enhancements

- Automate data ingestion with Azure Data Factory pipelines
- Implement data quality checks with Azure Synapse
- Add automated NER annotation pipeline
- Set up monitoring and data lineage tracking
- Implement Infrastructure as Code (Bicep/Terraform)

## Infrastructure as Code
The ARM template for this Data Lake setup is available in /infrastructure/template.json.
### Key Configuration
```json
{
  "Hierarchical Namespace": "Enabled (Data Lake Gen2)",
  "Encryption": "Microsoft-managed keys",
  "Network Access": "Public endpoint, Azure Services allowed",
  "Soft Delete": "7 days retention",
  "TLS Version": "1.2 minimum"
}
```
Deploy This Template
```bash
az deployment group create \
  --resource-group <YOUR_RESOURCE_GROUP> \
  --template-file infrastructure/template.json \
  --parameters storageAccounts_cvdatastoragetotest_name=<YOUR_STORAGE_NAME>
```
## Data Schema
### Bronze Layer

- Raw CSV/JSON files with NER annotations
- Fields may include: text, entities, labels, spans
- Data quality: Inconsistent, may have nulls and errors

### Silver Layer

- Cleaned and validated NER datasets
- Standardized format
- Removed duplicates and invalid entries

### Gold Layer (Planned)

- Fully annotated NER training data
- Quality score for each annotation
- Ready for ML model consumption

## 🌱 Lessons Learned

- **Medallion Architecture** - Understanding the bronze/silver/gold pattern for organizing data at different quality levels
- **Data Lake Gen2** - Importance of hierarchical namespace for efficient data organization
- **Manual vs Automated** - While manual setup works for learning, automation is essential for production
- **Azure Portal Navigation** - Gained familiarity with Azure's storage and data services

## Next Steps

### Automation

Create Azure Data Factory pipelines for automated data ingestion
Implement data quality checks in the pipeline
Schedule regular data processing jobs


### Infrastructure as Code

Convert manual setup to Bicep templates
Version control all infrastructure changes
Enable reproducible deployments


### Data Processing

Complete NER annotation for gold layer
Implement data validation rules
Add data quality metrics and monitoring


### Analytics

Connect Azure Synapse for data analysis
Create dashboards for data quality metrics
Implement data lineage tracking



## 🏗️ Repository Structure
```
azure-datalake-ner/
├── README.md
├── infrastructure/
│   └── template.json          # ARM template for storage account
├── docs/
│   ├── setup-guide.md         # Detailed setup instructions
│   └── architecture.png       # Architecture diagram (TBD)
└── scripts/                   # Future: automation scripts
    └── data-processing/
```
## 🔑 License
MIT License
## 📇 Contact
Yussufkadir Syurmen

>[!NOTE]
>This is a learning project demonstrating data lake concepts and the medallion architecture pattern. The manual setup process documented here serves as a foundation for understanding before implementing full automation.
