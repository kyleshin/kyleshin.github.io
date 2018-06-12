---
layout: post
title: "How To Create Text Insets In UILabel"
date: 2018-06-12
comments: false
---
## How To Create Text Insets In UILabel

Suppose you need a left aligned label. UILabel would render the first letter right
at the edge of the label, as shown below.

![ugly label](/images/blog/2018-06-12/ugly_label.png)

If you don't have the option of repositioning the label to create extra room,
your solution may require you to create an inset for UILabel.
 There are two ways to achieve that.

1) Use Attributed String and set paragraph style

2) Subclass UILabel


## 1) Use Attributed String

Adding text inset for attributed string is just a matter
of setting up a paragraph style.

```swift
//set the paragraph style
let paragraphStyle = NSMutableParagraphStyle()
paragraphStyle.alignment = .left
paragraphStyle.firstLineHeadIndent = 10 //indent for the first line
paragraphStyle.headIndent = 10          //indent after the first line
                                        //you can also set a tailIndent if necessary

let attributedString = NSAttributedString(string: "Hello", attributes: [NSAttributedStringKey.paragraphStyle: paragraphStyle,
NSAttributedStringKey.foregroundColor: UIColor.white])

//add the attributed text to the label
let leftLabel = UILabel()
leftLabel.backgroundColor = .black
leftLabel.attributedText = attributedString
```

The label looks like this now. Much better.

<image src="/images/blog/2018-06-12/attributed_text.png" width = "50%">
</image>

## 2)Subclass UILabel

Another way to achieve the desired result is to subclass UILabel and override
drawText(in rect:)

```swift
class InsetLabel: UILabel {

    override func drawText(in rect: CGRect) {
        let inset = UIEdgeInsetsMake(0, 10, 0, 0)
        super.drawText(in: UIEdgeInsetsInsetRect(rect, inset))
    }

}

```

I'll look the same as the above image, so I won't repost the image.

## Final Thoughts

While not technically a solution for UILabel, it is worth mentioning using UIButton and set it's
edgeInsets properties could produce the desired result (there are three properties, handling image insets, title
  insets, and the combined insets). What you use is up to you.
