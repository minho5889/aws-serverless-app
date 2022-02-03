2-3 Improving IAM permission

Tuesday, August 24, 2021

11:39 AM

 

So far, we're using the generic store role which has full access

and this is not a good practice. So let's go back to the IAM

 

> \*Instruction

1.  Create a role

2.  attach a policy (only for 'get' and 'scan')

>  
>
>  

<img src="media/image1.png" style="width:6.45833in;height:3.5in" alt="Policies &gt; dynamodb-get-scan Summary policy ARN Description Permissions policy usage Policy summary { } JSON Tags policy versions Edit policy Delete policy Access Advisor o &#39;I: 2e12-1e-17&quot; , &quot;Statement&quot; : &quot;Sid&quot;• &quot;VisualEditore&#39;I , &quot;Effect&quot; : &quot;Allow&quot; , &quot;Action &quot; : &quot;dynamodb : Getltem&#39;l , &quot;dynamodb : Scan &quot; &#39;V Resource&quot; : &quot; arn : dynamodb: us-east-2: 383326505630: table/compare -yourself&quot; " />

Principle of least privilege

Now we have a better control over which function is allowed to do what and this is a good practice since we have clear permissions settings and no overlapping and no function is allowed to do more than it needs to do.
