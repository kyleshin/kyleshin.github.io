---
layout: post
title: "Self Sizing Table View Cells"
date: 2019-01-02
author: Kyle Shin
comments: true
---

In today's post, we will learn about automatic self sizing table view cells. It is quite easy to implement, and this will go perfectly
with dynamic text size.

## Our Sample Project
Imagine we are building an application with a post feed. Each post will contain a profile image, user name,
a text body, and some reaction buttons. The name could be short or very long. The same goes with the text body, which could vary from a single line
to multiple lines. iOS now makes it incredibly easy to let table view adjust sizes on it's own. We just need to enter a few lines of
code to help it along.

Please note since the purpose is to demonstrate self sizing cells and dynamic text size, I have not styled this demo for looks.
In fact, I have given labels and textViews different background color so they would stand out. They look ugly, but it would make clear
to us the bounding size of the views.

The sample code for this project is posted at https://github.com/kyleshin/demo-selfSizingTableViewCell .
You can download the code to follow along. Note since there are quite a few good tutorials already using storyboard, this tutorial will use
programmatic layout. Thus we will configure everything in code.

## The Layout

The cell will have one image view, we will just populate it with a standard default image.
Cell will contains name label on top, body text view in the middle, and buttons contained in a stackview at the bottom

Here's how the end result would look like. Notice they respond to different font sizes.
As you can see, the cells resizes not only to the different sizing need of the name and body text, but also to font sizes.
<image src="/images/blog/2019-01-02/1.png" width = "25%"></image> <image src="/images/blog/2019-01-02/2.png" width = "25%"></image>

## The Code


Let's start with the table view controller(ViewController.swift). Inside viewDidLoad, add these two lines of code:

<!-- code -->
<pre><code class="line-numbers language-swift">tableView.rowHeight = UITableView.automaticDimension
tableView.estimatedRowHeight = 200
</code></pre>
<!-- end code -->
The tableView.estimatedRowHeight should be close to the size of the final cell size. I picked 200.
That's it for the table view controller. Let's move on to the table view cell. We will need to do a few things to the label and textView.

For the cell (MyCell.swift), the most import thing is the make sure there is a continuous chain of layout constraint, from the top and leading side, to the bottom and trailing side. The layout codes are inside the layout() method.
<!-- code -->
<pre><code class="line-numbers language-swift">
func layout(){
    profileImageView.topAnchor.constraint(equalTo: topAnchor, constant: 5).isActive = true
    profileImageView.leadingAnchor.constraint(equalTo: safeAreaLayoutGuide.leadingAnchor, constant: 6).isActive = true
    profileImageView.heightAnchor.constraint(equalToConstant: 44).isActive = true
    profileImageView.widthAnchor.constraint(equalToConstant: 44).isActive = true

    name.topAnchor.constraint(equalTo: topAnchor, constant: 5).isActive = true
    name.leadingAnchor.constraint(equalTo: profileImageView.trailingAnchor, constant: 5).isActive = true
    name.trailingAnchor.constraint(equalTo: safeAreaLayoutGuide.trailingAnchor, constant: -30).isActive = true

    body.topAnchor.constraint(equalTo: name.bottomAnchor, constant: 5).isActive = true
    body.leadingAnchor.constraint(equalTo: name.leadingAnchor, constant: 0).isActive = true
    body.trailingAnchor.constraint(equalTo: name.trailingAnchor, constant: 0).isActive = true

    //we will place the upvote and downvote buttons into this stackview
    let buttonStackView = UIStackView(arrangedSubviews: [upvoteButton,downvoteButton])
    prepareViewsForLayout(views:buttonStackView)
    buttonStackView.axis = .horizontal
    buttonStackView.distribution = .fillEqually

    buttonStackView.leadingAnchor.constraint(equalTo: safeAreaLayoutGuide.leadingAnchor, constant: 55 ).isActive = true
    buttonStackView.trailingAnchor.constraint(equalTo: safeAreaLayoutGuide.trailingAnchor, constant: -30).isActive = true
    buttonStackView.heightAnchor.constraint(equalToConstant: 44).isActive = true
    buttonStackView.bottomAnchor.constraint(equalTo: safeAreaLayoutGuide.bottomAnchor, constant: -5).isActive = true
    buttonStackView.topAnchor.constraint(equalTo: body.bottomAnchor, constant: 0).isActive = true
}
</code></pre>
<!-- end code -->



There's also a few properties we need to set for the name label.:
<pre><code class="line-numbers language-swift">//important for self sizing
label.adjustsFontForContentSizeCategory = true
label.font = UIFont.preferredFont(forTextStyle: UIFont.TextStyle.body)
label.numberOfLines = 0
</code></pre>
This would also allow text size to be dynamic.

Similarly, the text view will have these properties:
<pre><code class="line-numbers language-swift">//important for self sizing
view.adjustsFontForContentSizeCategory = true
view.font = UIFont.preferredFont(forTextStyle: UIFont.TextStyle.body)
view.isScrollEnabled = false
</code></pre>

If you set the isScrollEnabled to true(that's default setting), then the automatic resizing wouldn't work.



## Conclusion

As you can see, implementing self sizing table view cells is quite simple. It's simply a matter of making sure all the checkboxes are checked.
