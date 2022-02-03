1-5 Models(compare data)

Monday, August 23, 2021

9:56 PM

 

**Integration Request**

 

<img src="media/image1.png" style="width:5.18056in;height:2.25in" alt="application/json Generate template: CompareData 1 $input .path( $ • ) ) &quot;height&quot; : a &quot; 1 ncome&quot; " />

Line 1: Setting our own variable which we can use inside of the template, the inputRoot variable, this is a variable which you could rename, that's no reserved name

 

What it does here is it simply extracts the request body with this path method here. Before we used $input.json('$'), we're using path in the end here, this will give us the same, it will give us access to our request body.

<img src="media/image2.png" style="width:5.3125in;height:1.86806in" alt="application/json Generate template: 1 = $i nput. path(&#39;$ • ) ) &quot;age&quot; : SinputRoot.agel " />

 

So now we will make sure that lambda only gets an age property which holds, well the value of our actual age property we have on the request body.

 

{

"your-age": $input.json('$')

}

 

 

{

"name" : "Bruce Wayne",

"alias" : "Batman",

"attack" : 85,

"defence" : 55

}

 

\#set($inputRoot = $input.path('$'))

{

"2x-attack-booster" : $inputRoot.defence

}
