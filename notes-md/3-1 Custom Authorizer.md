3-1 Custom Authorizer

Tuesday, August 24, 2021

12:58 PM

What is a custom authorizer?

A custom authorizer uses lambda behind the scenes.

 

It tells API Gateway to call a specific lambda function, pass some data, some information from the incoming request to that function. The function then has to run some code to validate or to identify that user.

<img src="media/image1.png" style="width:6.13194in;height:6.50694in" alt="Authorizers Authorizers enable you to control access to your APIs using Amazon Cognito user Pools or a Lambda function. + Create New Authorizer Create Authorizer Name • Type * O Lambda Lambda Function • O Lambda Invoke Role O Lambda Event Payload * O Token Source&#39; O Authorization Caching O Enabled Create Cognito Request Token Validation O TTL (seconds) Cancel " /><img src="media/image2.png" style="width:2.625in;height:3.125in" alt="Return IAM Policy &quot;Effect&quot;: &quot;Allow&quot;, &quot;Action&quot;: &quot;execute-api&quot; Return Principal ID (User Id) mentation Return Context Object &quot;YourData&quot;: &quot;YourValue&quot;, Age&quot;: &quot;28&quot; " />

We need these

 

**Code**

<img src="media/image3.png" style="width:11.27083in;height:12.41667in" alt="1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 41 43 45 exports. handler = const token = / (Use token if(token = (event, context, callback) event . authorizationToken; &#39;allow&#39;) { const policy = genpolicy( &#39;allow&#39;, event.meth0dArn); // methodArn some information we get from API passed into this function const principalld = alsdjovdnkf&#39; ; const context = { simpleAuth: true const response = principalld: principalld, policyDocument: policy, context: context callback(null, response); else if (token — &#39;deny•) { const policy = genP01icy( &#39;deny&#39; , event . methodArn); // methodArn some information we get from API passed into this function const principalld = alsdjovdnkf&#39; ; const context = { simpleAuth: true const response = { principalld: principalld, policyDocument: policy, context: context callback(null, response) ; else { callback( &#39; Unauthorized &#39; ) ; function genP01icy(effect, resource) { const policy = policy .Version = 2912-10-17&#39; ; policy. Statement = [I; const stmt = stmt. Action = execute-api : Invoke ; stmt . Effect = effect; stmt. Resource = resource; policy. Statement . push ( stmt) ; return policy; " /><img src="media/image4.png" style="width:5.375in;height:3.27083in" alt="The following input data is provided to you: &quot;type&quot; ; &quot;TOKEN&quot; , &quot;authorizationToken&quot; : &quot;&lt;cal ler- suppli ed- token&gt;&quot; , &quot;methodArn&quot; : &quot;arn :aws : execute -api : : : capild &lt;caller- supplied-token&gt; is the token you actually receive. You configure how to extract the token from the incoming request in API gateway. methodArn simply refers to the endpoint on which this authorizer was triggered. " /><img src="media/image5.png" style="width:5.5in;height:6.5625in" alt="The following output data has to be provided by your function (via callback() &quot;principalld&quot;: &quot;yyyyyyyy% &quot;policyoocunent&quot;: { &quot;Version&quot; : &quot;2012-10-17&quot;, &quot;Statement&quot;: [ // The principal user identification &quot;Action&quot;: &quot;execute-api : Invoke&quot; , &quot;Allowl Deny&quot; , &quot;Effect&quot;: &quot;Resource : &quot; &quot;arn: aus :execute-api : cregionld&gt;: caccountld&gt;: &quot;context&quot;: { &quot;stringKey&quot;: &quot;value&quot;, &quot;numberKey&quot;: &quot;I&quot; , &quot;booleanKey&quot; : &quot;true&quot; principalld simply is the user identifier. policyDocument is a JS object which uses the IAM policy structure (as shown in the above example). context is the only optional attribute. It simply is an object of key-value pairs of your choice. " />
