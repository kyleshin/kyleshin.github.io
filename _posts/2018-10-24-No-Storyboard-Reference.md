---
layout: post
title: "How To Start iOS App Without Storyboard"
date: 2018-10-24
author: Kyle Shin
comments: true
---
This is a reference to starting a project in iOS without storyboard. The code is straight forward.

First thing first, you can delete the Main.storyboard file.

Second, go to General -> Deployment Info and delete the "Main" from Main Interface.
<image src="/images/blog/2018-10-24/img1.png" width = "95%"></image>

Third, add the following code in the AppDelegate.

## View Controller


<!-- code -->

<pre><code class="line-numbers language-swift">
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    //add the following code
    window = UIWindow(frame: UIScreen.main.bounds)      
    let homeVC = ViewController()         //make a UIViewController here, I'm using my custom class named ViewController
    window?.rootViewController = homeVC   //set it as window's root view controller
    window?.makeKeyAndVisible()           //make it visible
    return true
}

</code></pre>
<!-- end code -->
## Navigation VC

Launch navigation controller is similar:

<pre><code class="line-numbers language-swift">
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    //Similar to above, we assign navigation view controller as the root view controller
    window = UIWindow(frame: UIScreen.main.bounds)

    //construct our navigation controller
    let homeVC = ViewController()
    let navigationVC = UINavigationController(rootViewController: homeVC)

    //set our navigation controller as root view controller
    window?.rootViewController = navigationVC
    window?.makeKeyAndVisible()
    return true
}
</code></pre>

## Tab Bar VC

Let's do a tab bar controller, with first tab being a nav controller, and second tab just a
regular controller.

<pre><code class="line-numbers language-swift">
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    //Similar to above, we assign navigation view controller as the root view controller
    window = UIWindow(frame: UIScreen.main.bounds)

    //construct our first VC, which is a navigation controller
    let homeVC = UIViewController()
    homeVC.view.backgroundColor = .red
    let firstVC = UINavigationController(rootViewController: homeVC)
    firstVC.tabBarItem.title = "First Tab"

    //construct our second VC, just a normal view controller
    let secondVC = UIViewController()
    secondVC.view.backgroundColor = .blue
    secondVC.tabBarItem.title = "Second Tab"

    //create the tab bar controller, and pass in our view controllers
    let tabBarVC = UITabBarController()
    tabBarVC.setViewControllers([firstVC, secondVC], animated: false)

    //make the tab bar controller as the root view controller
    window?.rootViewController = tabBarVC
    window?.makeKeyAndVisible()
    return true
}
</code></pre>

## Conclusion

It's easy to launch an app without storyboard. I hope this reference comes handy for you.
