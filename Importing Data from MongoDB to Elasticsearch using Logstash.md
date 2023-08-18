# Importing Data from MongoDB to Elasticsearch using Logstash

This guide provides a step-by-step process to import data from MongoDB to Elasticsearch using Logstash. This is particularly useful when you have data in MongoDB and want to leverage the powerful search capabilities of Elasticsearch.

## Prerequisites

- MongoDB with data
- Elasticsearch
- Logstash

## Step 1: Export Data from MongoDB

Before importing data into Elasticsearch, you need to export it from MongoDB. Use the `mongoexport` command to achieve this:

```shell
D:\MongoDB\bin> .\mongoexport --db cartoonsDB --collection cartoons --out cartoons.json
```

This command exports the data from the `cartoons` collection in the `cartoonsDB` database to a file named `cartoons.json`.

## Step 2: Set Up Logstash Configuration

Create a configuration file for Logstash to specify the input, filter, and output settings. Here's an example configuration named `json_import.conf`:

```plaintext
input {
  file {
    path => "D:/MongoDB/bin/cartoons.json"
    start_position => "beginning"
    sincedb_path => "NUL"
    codec => json
  }
}

filter {
  json {
    source => "message"
  }
  mutate {
    rename => { "_id" => "mongo_id" }
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "cartoons"
    document_type => "data"
    user => "elastic" 
    password => "tz++ze-4DhDveK4vzXRO" 
  }
}
```

Make sure to adjust the path and authentication details as per your setup.

## Step 3: Run Logstash with the Configuration

Navigate to the Logstash directory and run the following command:

```shell
cd D:\logstash-8.9.0
bin\logstash -f json_import.conf
```

This will start Logstash and begin importing the data from the `cartoons.json` file into Elasticsearch.

## Step 4: Verify Data in Elasticsearch

You can use tools like Postman or Kibana to verify that the data has been successfully imported into Elasticsearch. If using Postman, send a GET request to `http://localhost:9200/cartoons/_search` to view the data in the `cartoons` index.

## Notes

- If you want to re-import the data, make sure to delete the existing index in Elasticsearch to avoid any conflicts or duplicates.
- Always backup your data before performing any import or delete operations.
