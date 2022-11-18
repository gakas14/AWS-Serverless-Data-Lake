# AWS-Serverless-Data-Lake

In this workshop, I ingested streaming data from the Kinesis Data Generator (KDG) into Amazon S3. 
then created a big data processing pipeline without servers or clusters, which is ready to process huge amounts of data. I also created an AWS Glue transform job to perform basic transformations on the Amazon S3 source data.
and finaly, I used a larger public dataset with more tables to observe the various AWS services in collaboration using AWS Athena.


1.  Create a CloudFormation template and uplode this file (serverlessDataLakeDay.json)
2. Create Kinesis Firehose Delivery Stream to Ingest data into your Data Lake

<img width="1269" alt="Screen Shot 2022-11-18 at 3 45 07 PM" src="https://user-images.githubusercontent.com/74584964/202648990-a0383525-6e2d-42e4-918c-b2a677cc1635.png">

3. Install the Kinesis Data Generator Tool (KDG)
<img width="1168" alt="Screen Shot 2022-11-18 at 3 45 57 PM" src="https://user-images.githubusercontent.com/74584964/202649439-55ef1789-1a42-49b4-bcce-46ad8e052c4e.png">

 Monitoring for the Firehose Delivery Stream
<img width="891" alt="Screen Shot 2022-11-18 at 3 46 15 PM" src="https://user-images.githubusercontent.com/74584964/202649517-8c0485c7-e9a5-43cb-bc98-e1795fe229a8.png">

Amazon Kinesis Firehose writes data to Amazon S3
<img width="1251" alt="Screen Shot 2022-11-18 at 3 47 52 PM" src="https://user-images.githubusercontent.com/74584964/202649610-8281f5da-9da0-4840-b980-0a4896f703bf.png">

4. Cataloging your Data with AWS Glue
  - Create crawler to auto discover schema of your data in S3

<img width="1267" alt="Screen Shot 2022-11-18 at 3 55 17 PM" src="https://user-images.githubusercontent.com/74584964/202650222-5b5f9847-78a9-445e-b103-e31ff1009ae5.png">
  
   - Create a database and a table then Edit the Metadata Schema
      
   
5. Create a Transformation Job with Glue Studio
  <img width="1251" alt="Screen Shot 2022-11-18 at 4 00 28 PM" src="https://user-images.githubusercontent.com/74584964/202651242-cd1bcb29-ba09-4b4b-8212-2986ba239059.png">
  
  <img width="1201" alt="Screen Shot 2022-11-18 at 4 01 24 PM" src="https://user-images.githubusercontent.com/74584964/202651251-8d081150-cacd-4f26-bc5d-58bef371a146.png">
  
6. SQL analytics on a Large Scale Open Dataset usimg AWS Athena

 - create a database
    CREATE DATABASE gdelt;
 
 - Create Metadata Table for GDELT EVENTS Data
  CREATE EXTERNAL TABLE IF NOT EXISTS gdelt.events (
        `globaleventid` INT,
        `day` INT,
        `monthyear` INT,
        `year` INT,
        `fractiondate` FLOAT,
        `actor1code` string,
        `actor1name` string,
        `actor1countrycode` string,
        `actor1knowngroupcode` string,
        `actor1ethniccode` string,
        `actor1religion1code` string,
        `actor1religion2code` string,
        `actor1type1code` string,
        `actor1type2code` string,
        `actor1type3code` string,
        `actor2code` string,
        `actor2name` string,
        `actor2countrycode` string,
        `actor2knowngroupcode` string,
        `actor2ethniccode` string,
        `actor2religion1code` string,
        `actor2religion2code` string,
        `actor2type1code` string,
        `actor2type2code` string,
        `actor2type3code` string,
        `isrootevent` BOOLEAN,
        `eventcode` string,
        `eventbasecode` string,
        `eventrootcode` string,
        `quadclass` INT,
        `goldsteinscale` FLOAT,
        `nummentions` INT,
        `numsources` INT,
        `numarticles` INT,
        `avgtone` FLOAT,
        `actor1geo_type` INT,
        `actor1geo_fullname` string,
        `actor1geo_countrycode` string,
        `actor1geo_adm1code` string,
        `actor1geo_lat` FLOAT,
        `actor1geo_long` FLOAT,
        `actor1geo_featureid` INT,
        `actor2geo_type` INT,
        `actor2geo_fullname` string,
        `actor2geo_countrycode` string,
        `actor2geo_adm1code` string,
        `actor2geo_lat` FLOAT,
        `actor2geo_long` FLOAT,
        `actor2geo_featureid` INT,
        `actiongeo_type` INT,
        `actiongeo_fullname` string,
        `actiongeo_countrycode` string,
        `actiongeo_adm1code` string,
        `actiongeo_lat` FLOAT,
        `actiongeo_long` FLOAT,
        `actiongeo_featureid` INT,
        `dateadded` INT,
        `sourceurl` string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES ( 'serialization.format' = '\t',
            'field.delim' = '\t')
LOCATION 's3://gdelt-open-data/events/';
  
  - Create Metadata Table for GDELT Lookup Tables
  <img width="924" alt="Screen Shot 2022-11-18 at 4 05 48 PM" src="https://user-images.githubusercontent.com/74584964/202652225-6dd12a15-4ae4-4d60-9d1f-2e12dba2259f.png">
  
  <img width="915" alt="Screen Shot 2022-11-18 at 4 05 54 PM" src="https://user-images.githubusercontent.com/74584964/202652239-99ca12c9-9d15-49d0-9584-b366ac024670.png">

<img width="917" alt="Screen Shot 2022-11-18 at 4 05 59 PM" src="https://user-images.githubusercontent.com/74584964/202652254-b178f6e3-5f2d-4705-ac0d-21c8f3b396f2.png">

<img width="916" alt="Screen Shot 2022-11-18 at 4 06 05 PM" src="https://user-images.githubusercontent.com/74584964/202652271-e8e32ed8-f3ca-423c-b236-c49384c4e81c.png">

  - Example output:
  <img width="785" alt="Screen Shot 2022-11-18 at 4 08 06 PM" src="https://user-images.githubusercontent.com/74584964/202652569-bd806688-93e5-4e43-bb80-f748418641a0.png">

<img width="789" alt="Screen Shot 2022-11-18 at 4 08 14 PM" src="https://user-images.githubusercontent.com/74584964/202652586-f02fa64b-11f5-4aa2-852d-185108d1ad11.png">


<img width="691" alt="Screen Shot 2022-11-18 at 4 08 24 PM" src="https://user-images.githubusercontent.com/74584964/202652595-1d25b22f-cb17-468b-b5f0-d07cac5c1057.png">


<img width="698" alt="Screen Shot 2022-11-18 at 4 08 32 PM" src="https://user-images.githubusercontent.com/74584964/202652621-790b106f-94e2-495c-83c4-68f02d609a11.png">
