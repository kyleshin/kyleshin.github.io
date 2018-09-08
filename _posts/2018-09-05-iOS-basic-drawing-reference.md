---
layout: post
title: "iOS Basic Drawing Reference"
date: 2018-09-05
author: Kyle Shin
comments: true
---
## iOS Basic Drawing Reference

Today's post will be a quick guide on basic drawing in iOS.

Create a new single view controller project. Create a new swift file subclassing UIView in your project, let's call it DrawingPad.

We add @IBDesignable before the class keyword. We will also want to override the draw(\_ rect:) method. Our drawing code will go inside there.

<image src="/images/blog/2018-09-06/1.png" width = "95%"></image>

<br>


@IBDesignable will allow xcode to draw to the storyboard as we type in our DrawingPad class. To complete this, we will need to have one of the UIView be our custom class DrawingPad. For convenience of this project, we can let the content view of our default view controller be the DrawingPad class

<image src="/images/blog/2018-09-06/2.png" width = "95%"></image>

<br>

I tend to build most of my views in code and not with storyboard, so I cannot take advantage of @IBDesignable in the production project. However, I would often open a project to the side, similar to what we are doing now, to take advantage of the power and convenience of @IBDesignable. It's incredibly convenient and time saving to see the drawing displayed as I code, without having to run the project in simulator. (For whatever reason, my playground constantly crash 😅 , which is why I prefer to do drawing code this way).

Let's get started by drawing a straight line.

### Basic - Draw a straight line

From this point on, all the drawing code should be done within our draw(\_ rect:) method.

<pre><code class="line-numbers language-swift">// 1 - get the context

let context = UIGraphicsGetCurrentContext()!

//2 - set stroke color and line width
//    notice the use of cgColor
context.setStrokeColor(UIColor.red.cgColor)
context.setLineWidth(4.0)

//3 - plot the path, then stroke it
//    this is a straight line from (0,4) to (100,4)
context.move(to: CGPoint(x: 0, y: 4))
context.addLine(to: CGPoint(x: 100, y: 4))

context.strokePath()

</code></pre>

The code will produce the following image in your storyboard:

<image src="/images/blog/2018-09-06/3.png" width = "95%"></image>

<br>

A few things to note about the stroke width. That width is wrapped around evenly around the path
you selected. So in our example, our line goes from (0,4) to (100,4),2 points of width would go above our line, and 2 points of width below the line.

There are other ways to add lines. Add the following code after context.strokePath() from above.

<pre><code class="line-numbers language-swift">

context.setStrokeColor(UIColor.blue.cgColor)
let lines = [
    CGPoint(x: 0, y: 24),
    CGPoint(x: 100, y: 24),
    CGPoint(x: 100, y: 54)
]

context.addLines(between: lines)
context.strokePath()

</code></pre>

Now we have the following:

<image src="/images/blog/2018-09-06/4.png" width = "95%"></image>

<br>

Notice even though both the red and blue line x value is 100 at the second point, the blue line looks a tad bit longer
along the x-axis than the red line. This is from what we talked about earlier, because of the stroke width goes around the line.
If you change the x value of blue line to 98, you will see it aligns perfectly to the red line
<image src="/images/blog/2018-09-06/5.png" width = "95%"></image>

### Rectangle

The following code produce rectangles. We fill one, and stroke the path of another.

<pre><code class="line-numbers language-swift">

context.setFillColor(UIColor.red.cgColor)
context.setLineWidth(2.0)

//add rect and fill
context.addRect(CGRect(x: 4, y: 4, width: 50, height: 50))
context.fillPath()

//use convenience method
context.setStrokeColor(UIColor.blue.cgColor)
context.stroke(CGRect(x: 60, y: 4, width: 50, height: 50), width: 4.0)

</code></pre>

<image src="/images/blog/2018-09-06/6.png" width = "95%"></image>

<br>

### Circle

The following code produce circles and lines along the circle.

<pre><code class="line-numbers language-swift">

context.setStrokeColor(UIColor.blue.cgColor)
context.setLineWidth(2.0)

//blue circle
context.addEllipse(in: CGRect(x: 4, y: 4, width: 50, height: 50))
context.strokePath()

//black circle
context.setStrokeColor(UIColor.black.cgColor)
context.strokeEllipse(in: CGRect(x: 64, y: 4, width: 50, height: 50))

//red arc along the circle
context.setStrokeColor(UIColor.red.cgColor)
context.addArc(center: CGPoint(x: 30, y: 90), radius: 25, startAngle: CGFloat.pi / 4.0, endAngle:CGFloat.pi * 3 / 4.0 , clockwise: true)
context.strokePath()

</code></pre>

<image src="/images/blog/2018-09-06/7.png" width = "95%"></image>

<br>

### Bezier Path

We can draw a curve by providing a starting and ending points. We then provide control point(s). I always image the bezier curve like a piece of stretched out (physical)string,
and the control points are where we tuck the string towards. Let's try a piece of code and see how it looks:

<pre><code class="line-numbers language-swift">

context.setStrokeColor(UIColor.black.cgColor)
context.setLineWidth(3.0)

let start = CGPoint(x: 4.0, y: 4.0)
let end = CGPoint(x: 4, y: 100)
let controlPoint = CGPoint(x: 50, y: 50)
context.move(to: start)
context.addQuadCurve(to: end, control: controlPoint)
context.strokePath()

</code></pre>

<image src="/images/blog/2018-09-06/8.png" width = "95%"></image>

<br>

Experiment with the control point. How does it look when the point is (50,25)?
(25,50)? Plug a few points in so you can grasp intuitively how the curve is effected by the control point.

### Conclusion

Drawing is really fun and easy in iOS when performed in the draw(\_ rect:) of UIView subclass. The best way to learn is to play and experiment.
Just remember the basic steps: get context, set color and line width. Set points or shape, then stroke or fill.
