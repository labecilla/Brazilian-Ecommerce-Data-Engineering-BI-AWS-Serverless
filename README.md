# Ecommerce-Data-Engineering-BI-AWS-Serverless

SECTION 1: DWH
1. Create MySQL RDS instance to import raw transactional data.
2. Historical: Create a Data Pipeline job to import raw data from RDS to S3 bucket in csv format.
 - Apply simple transformations like joining tables with same level of grain like one to one relationship.
3. Historical: Create a redshift cluster, staging and production databases then import data from s3 bucket using the copy command.
4. Incremental: Create a Data Pipeline job to import current raw data from RDS to S3 bucket in csv format.
5. Incremental: Create a glue job (Spark or Python Shell) to import current raw data from S3 bucket to redshift staging then production databases.
 - Use staging to store current data, compare with production, delete duplicate data in production, insert data from staging to production, and then truncate staging.
 - Apply business transformations.
6. Create a lambda function to trigger incremental glue job everytime the incremental data pipeline job runs and updates the csv file in the s3 bucket.

SECTION 2: ETL
1. Test data in local system by creating a PySpark script that converts csv source data from local to parquet format in local.
2. Modify ETL script to run in a Glue job from s3 csv input to s3 parquet output.
3. Create a lambda function that triggers the Glue ETL job for any event in the s3 source bucket.
4. Create glue crawler to create data catalog from s3 bucket.
5. Query tables in Athena. Data scanned is smaller in parquet because of partitions and columnar storage.

SECTION 3: Centralization (Redshift Spectrum)
1. Run create external schema script in Redshift spectrum to create a schema from data catalog as if the data resides in a redshift cluster.
2. You can now create cross database joins between tables currently in Redshift and saved in Glue data catalog.
3. Optional: Run create external table script in Redshift spectrum to create a table directly from csv files stored in an s3 bucket/data lake.

SECTION 4: Write directly to Redshift
1. Create external schema and table in Redshift.
2. Create an ETL script to run in a Glue job from s3 csv input to Redshift.
3. Query the table in Redshift.
