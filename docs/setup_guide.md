# Setup Guide

## Overview
This project documents an Azure Data Lake Storage Gen2 implementation built using the Azure Portal.

## Architecture Components

### Azure Resources Created
- **Storage Account:** Data Lake Storage Gen2
- **Container:** `[your-container-name]`
- **Access Tier:** Hot/Cool
- **Replication:** LRS/GRS

## Recreating This Setup

### 1. Create Storage Account

1. Navigate to Azure Portal
2. Click "Create a resource" → "Storage account"
3. Configure:
   - Name: `[unique-name]`
   - Performance: Standard
   - Redundancy: Locally-redundant storage (LRS)
   - Enable hierarchical namespace: **Yes** (for Data Lake Gen2)

### 2. Create Container

1. In Storage Account, go to "Containers"
2. Click "+ Container"
3. Name: `datalake-container`
4. Public access level: Private

### 3. Configure Directory Structure

Created the following structure:
```
/raw/           - Raw ingested data
/processed/     - Cleaned and transformed data
/curated/       - Analytics-ready datasets
```

### 4. Set Access Policies

- Configured role-based access control (RBAC)
- Assigned "Storage Blob Data Contributor" role

## Data Organization

[Describe how you organized your data in the lake]

## Cost Optimization

- Used lifecycle management policies
- Set appropriate access tiers
