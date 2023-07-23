# Implementing and Running ElasticSearch on Windows 10

This guide will walk you through the steps to implement and run ElasticSearch on your PC. For this tutorial, I am using Windows 10 as my local environment.

## Step 1: Download Elasticsearch

The latest stable version of Elasticsearch can be found on the [Elasticsearch official website](https://www.elastic.co/downloads/elasticsearch). Download the .zip archive for Elasticsearch.

## Step 2: Unzip the File

Once the download is complete, unzip it with your favorite unzip tool. This will create a folder called `elasticsearch-<version>`, which we will refer to as `%ES_HOME%`. In my case, `D:\elasticsearch-8.8.2` is my `%ES_HOME%`.

## Step 3: Configure Elasticsearch to use HTTP

You can find a .yml file named `elasticsearch.yml` under the directory `D:\elasticsearch-8.8.2\config`. Open it and look for a setting named `xpack.security.http.ssl.enabled` and set it to `false`. If the setting doesn't exist, you can add it.

## Step 4: Run Elasticsearch and Check that Elasticsearch is Running

I use Postman to execute this step. Before this, we need to reset the password of the "elastic" user if you don't know the corresponding password. You can achieve this procedure through these commands:

```shell
cd D:\elasticsearch-8.8.2\bin
.\elasticsearch-reset-password.bat -u elastic
```
Through these two commands, you will successfully reset the password of the "elastic" user. Then, in Postman, you can follow these steps to check if ElasticSearch is running normally:


1. Open Postman and enter your Elasticsearch URL (either `http://127.0.0.1:9200` or `https://127.0.0.1:9200`, depending on your configuration).
2. In the Authorization tab, select Basic Auth from the Type dropdown menu.
3. Enter `elastic` as the username and the password you set during the Elasticsearch setup in the Password field.
4. Click Send to make the request.

If your ElasticSearch is running normally, you will get this response:

```json
{
    "name": "LAPTOP-CQBCU01J",
    "cluster_name": "elasticsearch",
    "cluster_uuid": "OA7PPkJwSTeGCKu-hTAEmw",
    "version": {
        "number": "8.8.2",
        "build_flavor": "default",
        "build_type": "zip",
        "build_hash": "98e1271edf932a480e4262a471281f1ee295ce6b",
        "build_date": "2023-06-26T05:16:16.196344851Z",
        "build_snapshot": false,
        "lucene_version": "9.6.0",
        "minimum_wire_compatibility_version": "7.17.0",
        "minimum_index_compatibility_version": "7.0.0"
    },
    "tagline": "You Know, for Search"
}
```
This indicates that your ElasticSearch has been successfully installed on your local environment.
