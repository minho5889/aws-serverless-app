1-4 BodyMappingTemplates

Monday, August 23, 2021

8:13 PM

 

<img src="media/image1.png" style="width:4.35417in;height:6.3125in" alt="Body Mapping Templates can be confusing, but in the end, they&#39;re not that difficult. You use the Apache Velocity Language when working with these templates, that Will only matter once you create more complex transformations though. Basic explanations (see below) should be relatively self-explanatory First, you need to understand that they simply allow you to control which data your action receives (e.g. Lambda). You can for example transform incoming data of the following shape: With the following template: &quot;*Tsonuæ&quot;: " /><img src="media/image2.png" style="width:5.59722in;height:6.3125in" />

 

 

**Why do we even use body mapping templates?**

In the integration request and response, we can use body mapping templates to map in the case of request, the data we pass to the action and in the case of response, data we get out of that action. So here integration request ,we can scroll down and first of all switch this to when there are no templates to defined

<img src="media/image3.png" style="width:5.97222in;height:6.28472in" />

This is forwarding a mapped template or a mapped event data object with data form that request which is also the reason why we wouldn't have to parse JSON data here because it already mapped Javascript object instead.

 

We just add a template call "application/json"

> \*\*\*Important\*\*\*

This name is not random! "application/json" means that incoming requests with "Content-Type" of "application/json" will be handled by this template!

』

 

**Let's make a template**

<img src="media/image4.png" style="width:5.95139in;height:2.29861in" alt="application/json Generate template: 2 &quot;body-json&quot;: S input. j son(&#39;$&#39;) " />

{

"age" :28,

"height" : 72,

"income" : 2500

}

 

{

"your-age": $input.json('$')

}

$input =&gt; Variable provided by AWS, gives you access to your request data (body, params, …)

 

json('$') =&gt; Extracts complete request body

 

<img src="media/image5.png" style="width:5.93056in;height:2.20139in" alt="application/json Generate template: 2 &quot;age&quot;: *input .json( &#39;S. person. age&#39;) " />

our template to extract 'age'

 

<img src="media/image6.png" style="width:2.89583in;height:4.27083in" alt="Request Body &quot;person&quot; • &quot;nane&quot; : &quot; &quot;age&quot; : 21 Test " /><img src="media/image7.png" style="width:2.54167in;height:1.96528in" alt="Request: /compare-yourself status: 200 Latency: 115 ms Response Body " />

 

CloudWatch logs

<img src="media/image8.png" style="width:9.44444in;height:0.75694in" alt="d263bcc2.gøc9-a91f.a91b-enbd5S2ggas INFO { age: 24 } : 21. OIBZ d263bcc2-8ec9-a97f- a91b-e33bd552gga5 INFO { age: 24 } " />

고

 

We have no other metadata about the requests because in our mapping template under integration request here, we only extract that and the difficult part is to grasp the language we use with this **$input.json('$')**

 

**Idea behind Body Mappings**

$input refers to request data (e.g. params, body)

 

'$' refers to just the request body and with '.' notation infers different level of layouts, meaning accessing data

 

In short,

We are basically restructuring the input data and mapping a complex data to an easier one.

 

There is a clear separation between API Gateway where we receive our request and work. And lambda where we expect to get data in a certain structure and then do something with it.

 

Therefore lambda that doesn't have to care about which structure our request has, an API Gateway simply needs to provide the right structure to lambda.

屯

 

**Mapping Response Data**

<img src="media/image9.png" style="width:5.64583in;height:2.02778in" />

=&gt; this is integration response mapping templates

 

$input is the callback info sent back by Lambda,

json('$') then gives us the data passed with the callback

 

<img src="media/image10.png" style="width:2.60417in;height:2.29167in" alt="Request: &#39;compare-yourself status: 200 Latency: 120 ms Response Body &quot;your-age&quot; • . 52 " /><img src="media/image11.png" style="width:2.95139in;height:1.625in" alt="Request Body &quot; person&quot; &quot;name&quot; • " />

 

This is how we can also map the response, lambda gives us a number but let's say our client, our application which calls the API in the end expects to get an object where this is stored in a your age property, nothing easier than that.

 

We don't have to adjust our lambda function to our client, we only have to adjust our API Gateway to our client and transform the data we get by lambda into the format we want to use and that's the power of body mapping templates.

 

We can clearly separate lambda from API Gateway and we can control what goes into lambda and what you do with what comes out of lambda.
