---
layout: post
title: "Loop Through Array"
date: 2018-10-02
author: Kyle Shin
comments: true
---
Looping through an array is a common task we do all the time.
Let's cover some ways to do this and observe the differences.

## For-In Loop With Value and forEach

First the for-in loop:

<!-- code -->

<pre><code class="line-numbers language-swift">
let names = ["Conor","Khabib","Nate","Tony"]

for name in names{
  print(name)
}

</code></pre>
<!-- end code -->


A closely related way is the forEach method:


<!-- code -->

<pre><code class="line-numbers language-swift">
names.forEach { name in
  print(name)
}

</code></pre>
<!-- end code -->

These two methods have one important difference. Unlike the for-in loop, forEach  
is unable to exit the loop early. Specifically:

1) The forEach closure cannot use the break or continue statement to exit the loop or skip subsequent calls.

2) Using return in the forEach will only exit the current call, not the subsequent call



<!-- code -->
## For-In Loop With Index
While for-in loop and forEach from the previous section offers a way to iterate and use the value from the array,
sometimes it may be more suitable to use index. We can do that this way:

<pre><code class="line-numbers language-swift">
for index in 0 ..< names.count {
  print("\(names[index]) is positioned at index \(index)")
}

</code></pre>

<!-- end code -->

We can also do this:
<pre><code class="line-numbers language-swift">
for index in names.indices {
  print("\(names[index]) is positioned at index \(index)")
}

</code></pre>
I tend to prefer names.indices over using the 0..<names.count. But that's a matter of
taste.

## Best of Both

This is my personal favorite, where we get both value and index of array.
We can do the following:

<!-- code -->

<pre><code class="line-numbers language-swift">
for (index,name) in names.enumerated(){
  print("\(name) is positioned at index:\(index)")
}

</code></pre>

<!-- end code -->

Since we are discussing Array, the index above is a true index. However,
it is **important** to note that is only true for sequences such as Array or
ContiguousArray. For some other type of collections, it could just be a counter. So we
have to be cognizant of that.

If we don't need the value or index, we can just replace the variable with _ .

This is still a for-in loop, so we can still use break and continue statements.

<!-- end code -->
