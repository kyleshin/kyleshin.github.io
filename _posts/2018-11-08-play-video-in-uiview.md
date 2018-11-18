---
layout: post
title: "Play Video In UIView"
date: 2018-11-08
author: Kyle Shin
comments: true
---
Here we will learn how to play video in a custom UIView subclass.
This technique is suggested here in the Apple Document:
https://developer.apple.com/documentation/avfoundation/avplayerlayer

## Our Custom Subclass

Let's create our custom subclass, per the suggestion.

<!-- code -->

<pre><code class="line-numbers language-swift">
import UIKit
import AVKit
import AVFoundation

class PlayerView: UIView {
    var player: AVPlayer? {
        get {
            return playerLayer.player
        }
        set {
            playerLayer.player = newValue
        }
    }

    var playerLayer: AVPlayerLayer {
        return layer as! AVPlayerLayer
    }

    // Override UIView property
    override static var layerClass: AnyClass {
        return AVPlayerLayer.self
    }
}
</code></pre>
<!-- end code -->

Nice. Let's use it.

<pre><code class="line-numbers language-swift">
import UIKit
import AVKit
import AVFoundation

class SimpleViewController: UIViewController {

  var player: AVPlayer?
  let playerView = PlayerView()

  override func viewDidLoad() {
      super.viewDidLoad()
      layoutUI()  // Place your playerView in your favorite spot. I'll skip over the details.
      initializePlayer()  
  }

  //This is what we are interested in for this blog.
  func initializePlayer(){
    //I'll load the video from asset library.
    let videoString:String? = Bundle.main.path(forResource: "demo", ofType: "mp4")
    guard let videoPath = videoString else { return }
    let videoUrl = URL(fileURLWithPath: videoPath)
    player = AVPlayer(url: videoUrl)

    //assign the AVPlayer to our playerView's playerLayer
    playerView.playerLayer.player = player
    playerView.player?.play()

  }

  func layoutUI(){
    // Place your playerView in your favorite spot. I'll skip over the details.
  }
}
</code></pre>


## Conclusion

That's a great way to play video in a subclass of UIView. Of course we didn't get into
the details of how to effectively manage playing videos. Perhaps we can visit that in a
future blog post.
