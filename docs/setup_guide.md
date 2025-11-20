# Setup Guide

## Prerequisites

Before you begin, ensure you have the following installed and configured:

- **Azure CLI** (version 2.0 or higher)
```bash
  az --version
```
- **Python 3.8+** (if you have Python scripts)
- **Git**
- **Active Azure Subscription** with contributor access

## Azure Resources Required

- Azure Resource Group
- Azure Data Lake Storage Gen2 account

## Installation Steps

### 1. Clone the Repository
```bash
git clone https://github.com/Yussufkadir/azure-data-lake-project
cd azure-data-lake-project
```

### 2. Configure Azure Credentials

Login to Azure:
```bash
az login
```

Set your subscription (if you have multiple):
```bash
az account set --subscription "<your-subscription-id>"
```

### 3. Create Configuration File

Copy the template configuration:
```bash
cp config.template.json config.json
```

Edit `config.json` with your Azure details:
```json
{
  "storage_account_name": "your-storage-account-name",
  "container_name": "your-container-name",
  "resource_group": "your-resource-group"
}
```

**Important:** `config.json` is in `.gitignore` and will not be committed.

### 4. Set Environment Variables

Create a `.env` file in the project root:
```bash
AZURE_STORAGE_CONNECTION_STRING="your-connection-string-here"
AZURE_STORAGE_ACCOUNT="your-storage-account"
AZURE_CONTAINER_NAME="your-container-name"
```

To get your connection string:
```bash
az storage account show-connection-string \
  --name <your-storage-account> \
  --resource-group <your-resource-group>
```

### 5. Deploy Infrastructure (Optional - if starting from scratch)

If deploying the Azure infrastructure from ARM template:
```bash
# Create resource group (if needed)
az group create \
  --name <your-resource-group> \
  --location westeurope

# Deploy infrastructure
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file infrastructure/template.json \
  --parameters @parameters.json
```

### 6. Install Python Dependencies (if applicable)
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 7. Run Docker Container (if applicable)
```bash
# Build the image
docker build -t azure-data-lake-project .

# Run the container
docker-compose up -d
```

## Verification

Test your setup:
```bash
# Test Azure connection
python scripts/test_connection.py

# Or manually verify
az storage container list \
  --account-name <your-storage-account> \
  --auth-mode login
```

## Common Issues

### Issue: Authentication Failed
**Solution:** Ensure you're logged in with `az login` and have the correct permissions on the resource group.

### Issue: Storage Account Not Found
**Solution:** Verify the storage account name in your config matches the actual Azure resource.

### Issue: Connection String Invalid
**Solution:** Regenerate your connection string from Azure Portal:
1. Go to Storage Account → Access Keys
2. Copy Connection String from Key1 or Key2

## Security Notes

⚠️ **Never commit these files to Git:**
- `.env`
- `config.json`
- `parameters.json`
- Any files containing credentials or connection strings

## Support

For issues or questions:
- Check existing [GitHub Issues]
- Review Azure documentation
- Contact: syurmen2@gmail.com
