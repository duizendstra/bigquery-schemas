# Google API BigQuery Schemas

This repository contains a collection of BigQuery table schemas for various Google APIs. These schemas can be used to create tables in Google's BigQuery data warehousing service for storing responses obtained from different Google APIs.

## Structure

The repository is structured as follows:
```
├── admin_directory  
│ ├── users.json 
│ ├── ... 
├── drive  
│ ├── files.json  
│ ├── ...
├── ...
```


Each subdirectory represents a different Google API (like 'admin_directory' for the Admin SDK Directory API, 'analytics' for the Google Analytics API, and so on). Within each subdirectory, there are JSON files representing different endpoints of the respective API (like 'users.json', 'groups.json', etc. for the Admin SDK Directory API).

## Usage

To use these schemas, follow these steps:

1. Clone this repository.
2. Use the JSON schema files to create tables in BigQuery.

Here's a Python snippet using the `google-cloud-bigquery` client library:

```python
from google.cloud import bigquery
import json
import requests

# Initialize a BigQuery client
client = bigquery.Client(project="[your_project_id")

# Define your dataset
dataset_ref = client.dataset('your_table_id')

# Define the URL to the schema file on GitHub
schema_file_url = 'schema_file_url'

# Fetch the raw content of the schema file
response = requests.get(schema_file_url)
schema_json = response.json()

# Convert the JSON schema to BigQuery SchemaField objects
schema = [bigquery.SchemaField.from_api_repr(field) for field in schema_json]

# Create a new table
table_ref = dataset_ref.table('your_table_id')
table = bigquery.Table(table_ref, schema=schema)
table = client.create_table(table)

print(f"Created table {table.project}.{table.dataset_id}.{table.table_id}")```

Replace 'your_project_id', 'your_dataset_id', 'schema_file_url', and 'your_table_id' with your dataset ID, the url to the schema file, and your table ID, respectively.

## Contributing
Contributions are welcome! Please feel free to submit a pull request with any corrections to existing schemas or addition of new ones.

## Disclaimer
This repository is not affiliated with, officially maintained by, or in any way officially connected with Google Inc. or any of its subsidiaries or its affiliates.
