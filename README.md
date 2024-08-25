# Building GenAI Data Apps with Snowflake and AWS Bedrock

## Introduction
Have you ever received marketing spam from a company and wondered why they sent you an email in a language you don't understand?
71% of customers dont want to recieve general mails, but want to be approached on a personal level and 78% of companies asked believe that by approaching customers in a personalized fashion will increase the chance a customer will repurchase if approached in a personalized fashion

In this demo, we will see how to build a GenAI Data app that provides a personalized reccomendation based on past purchases based on the integration between Snowflake Data Clud and AWS Services. We will stream data in near real time (purchases), use company information stoed in documents and GenAI technologies such as Large Language Models and Retrieval Augmented Generation to bring the latest information.

## Architecture
![](https://github.com/sfc-gh-mkobel/genai_dataapps_with_snowflake_and_amazon_bedrock/blob/main/images/demo_architecture.jpeg)

In this demo we have 3 key flows:

### Flow 1: Ingestion of purchase transactions from the Point of Sales systems to Snowflake Data Cloud.

The raw transactions are streamed in near real-time to the Bronze Layer using the integration between **Amazon Data Firehose** and **Snowflake Snowpipe Streaming**

__Amazon Data Firehose__ is a fully managed service that reliably loads real-time streaming data into data lakes, data stores, and analytics services. It can capture, transform, and deliver streaming data to destinations like Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and even third-party services such as Snowflake. With Firehose, you can easily stream data in near real-time without needing to manage the underlying infrastructure, making it a scalable solution for data ingestion and processing.

__Snowflake Snowpipe Streaming__ is a feature that allows you to ingest data in near real-time into Snowflake tables. It provides a way to continuously stream data from sources like event streams or IoT devices directly into Snowflake, enabling immediate querying and analysis. Snowpipe Streaming is designed for low-latency data ingestion, ensuring that your data is quickly available for downstream processing and analytics without the need for batch loading or manual intervention.

The transaction data is then organized using **Snowflake Dynamic Tables**

__Snowflake Dynamic Tables__ are a powerful feature that allows you to automatically keep tables updated with the latest data by continuously processing incoming data streams. Dynamic Tables are defined by a query, and Snowflake automatically manages the execution of this query as new data arrives, ensuring that the table's contents are always up-to-date. This feature is particularly useful for real-time analytics and data transformations, eliminating the need for manual refreshes or complex ETL pipelines.

### Flow 2: RAG Pipeline to ingest documents and prepare them for use in the GenAI data application

The retail company stored its documents describing the history of the company on **Amazon S3** these documents are streamed to Snowflake using **Snowflake Snowpipe**

__Amazon S3 (Simple Storage Service)__ is a scalable, high-speed, web-based cloud storage service designed for online backup and archiving of data and applications. It allows you to store and retrieve any amount of data at any time from anywhere on the web. S3 is highly durable, secure, and cost-effective, making it ideal for storing large datasets, media files, and backups. It also integrates seamlessly with other AWS services, enabling powerful data management and processing capabilities.



### Amazon Bedrock and Anthropic Claude 3
Amazon Bedrock is a fully managed service that makes it easy to build and scale generative AI applications using foundational models (FMs) from leading AI providers. It allows you to access models from providers like Anthropic, Stability AI, and others, along with AWS's own models. Bedrock simplifies the integration of generative AI into your applications by providing APIs for text, image, and other data types without needing to manage the underlying infrastructure.

Anthropic Claude 3 is a next-generation large language model (LLM) developed by Anthropic, known for its safety and alignment with human intentions. Claude 3 is designed to generate natural language text that is coherent, contextually relevant, and aligned with user input. It is part of the Claude family of models, which emphasize ethical AI usage and advanced reasoning capabilities, making it suitable for a wide range of applications, from customer support to creative writing.

in this solution will Amazon Bedrock with Anthropic Claude Sonnet 3.5 will be used to create the personalized email.
