2-2 Lambda code

Tuesday, August 24, 2021

6:57 AM

 

<img src="media/image1.png" style="width:7.03472in;height:1.89583in" alt="1 3 4 5 6 7 8 9 in&amp;x.js const AWS = require( taws-sdk&#39; ) ; const dynamoDB = new AWS.DynamoDB({region: &#39;use-east-2&#39; , exports. handler = (event, context, callback) =&gt; { console. log(event) ; const age = event. age; callback(null, age) ; apiVersion . • &#39;2012-08-10&#39;}); " /><img src="media/image2.png" style="width:0.375in;height:1.27083in" />

<img src="media/image3.png" style="width:2.13889in;height:1.39583in" />

 

Why do we need outside of handler function?

It's an advanced concept but in general, the code running here is not online all the time.

 

Whenever a trigger occurs running your lambda function, AWS quickly spins up like a server environment, some wrapper containing your lambda function.

 

This is really fast but it doesn't tear down this wrapper once your function finishes, it keeps it alive for a couple of minutes. Therefore if your function executes a couple of times in a short time span, it will reuse that wrapper.

 

Let's take advantage of this

If that wrapper is being started, it will execute everything in this file, not just your function handler.

 

If the wrapper is still up though, it will not re-execute the part outside of your function handler and that of course gives us a little performance edge.

 

If we put the code which doesn't need to get executed on each triggering event outside of that handler and that's just what we are doing here. Because importing the SDK and setting up the DynamoDB object, that's always going to be the same process, so we don't necessarily need to put that in our function handler.

 

<img src="media/image4.png" style="width:6.77778in;height:5.58333in" alt="1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 Execution results x const AWS = require( &#39; aws-sdk&#39;); const dynamodb = new AWS.DynamoDB({region: &#39;use-east-2&#39; , exports. handler = context, callback) { const params = Item: { &quot;Userld&quot;: { apiVersion. • &#39;2012-08-101}); S: &quot; askdfosjf&quot; &quot;Age&quot;: { &quot;Height&quot; : N: &quot;72&quot; &quot;Income&quot; : { N: &quot;2500&quot; TableName: &quot; compare-yourself&quot; dynamodb. putltem(params, function(err, if (err){ console. log(err) ; callback(); } else { console. log(data) data) ; callback(null, data) { " />

 

But we cannot test our lambda function because it gives us authorization error. So, We need to give a permission to test our code successfully.

below is basic execution role(default role)

<img src="media/image5.png" style="width:6.84028in;height:3.89583in" alt="Permissions Policy usage Policy summary JSON Tags Policy versions Access Advisor Edit policy &quot;version&quot; : &quot;2012-10-17&quot;, &quot; Statement&quot; : &quot; Effect&quot; : &#39;&quot;Allow&quot; , &quot;&#39;Action&quot;: &quot; logs : CreateLogGroup&quot; , &quot;Resource : &quot; &quot; arm : : logs : Us -east-2 3833265es63e: k&quot; &quot;Effect&quot; : &quot;Allow&quot; , &quot;Action &quot; : &quot;logs :CreateLogStream&quot; , &quot;10gs : PutLogEvents &quot; &quot;Resource&quot; &quot;arn: aws : logs : us -east -2: 383326505630 : log-group: / aws/lambda/ cy-store-data " />

 

> This allow us two things

1.  create a log group

2.  create a log stream

> So, We are going to attach a new policy which is
>
> 'AmazonDynamoDBFullAccess'

<img src="media/image6.png" style="width:5.91667in;height:4.47222in" alt="1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 25 26 27 28 29 30 31 inckx.js const AWS require( aws-sdk&#39; const dynamodb = new &#39; us-east-2&#39; , exports. handler = (event, context, callback) { const params = { Item: { &quot;Userld&quot; S: &quot;user_&quot; + Math. random() &quot;Age&quot;: { N: event. age &quot;Height&quot; N: event. height &quot; Income&quot;: { N: event. income apiVersion: &#39; 2012-08-10 • ; TableName: &quot;compare-yourself&quot; dynamodb. putltem(params, function (err, if (err) { console. log(err) ; callback(err) ; } else { console. log(data); callback(null, data); data) { " />

Now a better way though is to pass the right format by API Gateway then this whole body mapping template will make more sense.

 

If we visit the API Gateway, we can wrap our extraction of age, height and income here into quotation marks and this will now not pass a string which holds $inputRoot.age but it holds the value of that expression but as a string, you learned this in the API Gateway module.

 

So this now gives the mapping template a whole new sense. Because now, we not only extract data which would have been there before anyways but we also transformed the type of data and if we receive

a number, we automatically turn it into a string here already.

 

**Test Run**

<img src="media/image7.png" style="width:2.6875in;height:2.35417in" alt="Request: /compare-yourself Status: 200 Latency: 460 ms Response Body &quot;your-age&quot; " /><img src="media/image8.png" style="width:3.16667in;height:1.375in" alt="Request Body &quot;age&quot; : 48, &quot;height&quot; &quot;income&quot; : 1804 " />

 

<img src="media/image9.png" style="width:6.97917in;height:4.19444in" alt="compare-yourself Overview Items O Metrics Alarms Capacity Create item Actions v Scan: [Table] compare-yourself: Userld Indexes Height 72 72 69 Global Tables Income 1800 More v Viewing 1 to 3 items Sca n [Table] compare-yourself: Userld O Add filter Start search Userld O dasf787af8safa oanvosdjflj user 0.07026859306250022 Age 28 28 48 " />

 

Here, we get exactly the data we sent stored here without an error because we transformed into a string in the body mapping template of API Gateway and then we use this data here in lambda by accessing it on the event object.

 

This shows the full chain from sending data with API Gateway over transforming it to passing it to lambda, to using it there to create a new entry on DynamoDB.

 

 

Web Testing

<img src="media/image10.png" style="width:7.01389in;height:2.14583in" />

codepen.io

1

 

<img src="media/image11.png" style="width:3.77083in;height:0.39583in" /><img src="media/image12.png" style="width:1.92361in;height:5.875in" />

?

<img src="media/image13.png" style="width:2.60417in;height:1.07639in" alt="İframeCons01eRunner- İframeCons01eRunner- X04c013047d 712.js:1 auc013047d 712. is:ı " />

chrome

console

 

3

DynamoDB

<img src="media/image14.png" style="width:5.18056in;height:1.61111in" alt="Userld O dasf787af8safa oanvosdjflj Age 28 28 48 26 Height 72 72 69 58 Income 2500 2500 1800 user user 0.07026859306250022 0.295392264251503 " /><img src="media/image15.png" style="width:0.3125in;height:0.41667in" />
