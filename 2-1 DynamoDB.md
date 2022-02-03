2-1 DynamoDB

Monday, August 23, 2021

11:29 PM

 

<img src="media/image1.png" style="width:5.51389in;height:3.91667in" alt="How it works A NoSQL Database No Relations Data Format Key •r 23 Value " />

 

<img src="media/image2.png" style="width:5.35417in;height:0.59722in" />

has to be unique -&gt; uniquely identify data

why partition key?

 

fleet of SSD, partitioning state drive

best to have as many as partition key as possible

 

f

 

<img src="media/image3.png" style="width:5.59722in;height:3.0625in" alt="Keys, Attributes, Indices Always required: Partition Key Partition Key Primary Key UserlD Attribute FirstName Optional: Partition Key + Sort Key Sort Key Timestamp Global Secondary Index Local Secondary Index Partition Key Primary Key I — UserlD Attribute HeartRate " /><img src="media/image4.png" style="width:5.58333in;height:2.99306in" alt="AWS Dynamo DB + AWS Lambda Event Source Data Repository Ill/ Trigger Function Lambda Function Lambda Function Store &amp; Retrieve Data " />

 

<img src="media/image5.png" style="width:5.60417in;height:3.0625in" alt="NoSQL No Relations High Flexibility (No/ Weak Schemas) Data Repetition No Integrity Checks Easy Scalability NoSQLvs SQL SQL (Relational) Relations Limited Flexibility (Strong Schemas) No Data Repetition Integrity Checks Harder Scalability* " />
