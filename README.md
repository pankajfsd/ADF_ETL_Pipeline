# ADF_ETL_Pipeline

Project Details.
===============

1. As soon as the orders.csv file is uploaded in the blob storage. Both orders.csv from blob storage and order_items.csv from S3 will be ingested to ADLS Gen2.

2. My ingestion pipeline should trigger when orders.csv will be uploaded to the blob storage.

3. We will do some transformations(like aggregate,join,select) and divide the result in three categories:-

	a) high_value_orders(>500)

	b) low_value_orders(<=500)

	c) erroneous_orders(all the remaining which do not come under above two categories).

	-- Put these categorized data in the ADLS Gen2


4. Finally, We need to ingest the high_value_orders in SQL table for reporting purpose.


5. Resources Created

	a) blob storage
	b) data lake --> create container orders (directories --> orders, order_items)
	c) S3 bucket
	d) Azure Data Factory
	e) Key Vault
	f) linked services for --> Key Vault, S3, Data Lake, Blob Storage, sql database
	g) Corresponding Datasets --> ds_s3, ds_adls_order_items, ds_adls_orders, ds_sql_db, etc
	h) azure sql data base

CREATE TABLE premium_orders (
order_id INT NOT NULL,
order_date VARCHAR(45) NOT NULL,
order_customer_id INT NOT NULL,
order_status VARCHAR(45) NOT NULL,
order_amount float,
PRIMARY KEY (order_id)
);

6. Go to Data flows --> create transformations(to process the data)


7. pipelines
	a) pl_ingest_order_items_data (from S3 to adls(landing --> order_items folder))
	b) pl_ingest_orders_data (from blob to adls(landing --> orders folder))
	c) pl_process_orders_data
	d) pl_ingest_adls_to_sql

8. create an execute pipeline (to chain the pipelines using execute pipeline activity).

9. Create a trigger(storage event trigger) and attach it to the execute pipeline.

