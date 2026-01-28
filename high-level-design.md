Ingestion:
   Using Pub/sub for ingestion of the data as we have subscriber and publisher we can cretae topic and ingest the data to GCS
Using Dataflow creating the pipeline for ingestion of the data realtime streaming with the help pf apache spark

Following Kappa here 
GCS bronze layer:- for ingesting the raw data
GCS silver layer:- for cleaning up data by applying filters
GCS Gold layer:- cleaned and final data

BigQuery: - using Bigquery creating different data sets for keeping the bronze,silver and Gold layer data
with the help queries applying filter and cleaning the data

Cloud Composer: using Cloud composer we are add trigger for schduling the daily ingestion of data into bogquery

Looker/Vertex AI :- For analysing the Gold layer data
Monitoring : Monitoring the data if it fails so can track easily with help of logs
