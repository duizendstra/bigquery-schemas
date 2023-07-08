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

# Initialize a BigQuery client
client = bigquery.Client()

# Define your dataset
dataset_ref = client.dataset('your_dataset_id')

# Define the path to the schema file
schema_file_path = '/path/to/schema/file.json'

# Load the schema from the JSON file
with open(schema_file_path) as schema_file:
    schema_json = json.load(schema_file)
    schema = [bigquery.SchemaField.from_api_repr(field) for field in schema_json]

# Create a new table
table_ref = dataset_ref.table('your_table_id')
table = bigquery.Table(table_ref, schema=schema)
table = client.create_table(table)

print(f"Created table {table.project}.{table.dataset_id}.{table.table_id}")

Replace 'your_dataset_id', '/path/to/schema/file.json', and 'your_table_id' with your dataset ID, the path to the schema file, and your table ID, respectively.

## Contributing
Contributions are welcome! Please feel free to submit a pull request with any corrections to existing schemas or addition of new ones.

## Disclaimer
This repository is not affiliated with, officially maintained by, or in any way officially connected with Google Inc. or any of its subsidiaries or its affiliates.
