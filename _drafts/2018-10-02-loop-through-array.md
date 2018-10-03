---
layout: post
title: "Loop Through Array"
date: 2018-10-02
author: Kyle Shin
comments: true
---
## Loop Through Array

Looping through an array is a common tasks we do all the time.
Most could be accomplished this way.

<pre><code class="line-numbers language-swift">//method 1

let nameArray = ["Conor","Khabib","Nate","Daniel","Yamamoto"]

for name in nameArray{
  print(name)
}

//this will print all the names

</code></pre>

Nothing special there. Equally not special is looping through with an index:

<pre><code class="line-numbers language-swift">//method 2

let maxIndex = nameArray.count

for index in 0 ..< maxIndex {
  print(name)
}

//this will print all the names

</code></pre>

But we have an even more flexible way. Should you ever require the best of both worlds,
you can do the following:

<pre><code class="line-numbers language-swift">//method 3

for (index,name) in nameArray.enumerated(){
  print("\(name) is located at index:\(index)")
}
//this will print all the names, along with the index number

</code></pre>

Lastly, we can also loop this way.
