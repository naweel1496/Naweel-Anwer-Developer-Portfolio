---
layout: post
title: More flexible arrays in Swift
category: Swift
---

There comes a time where you have to create an array of objects which are not of same type but are some what similar.

## [AnyObject]
A strait solution to this type of problem is create an aray of AnyType and put anything you want into it. Some of us try to play safe by creating an array of nearest common ancestor type. For Eg. Say we want to have a list of all the components in Nav bar, we can create an array of `UIView`

## Protocol Oriented Solution
Simply create an array of type Protocol, and you can insert any object that conforms to the protocol.

{% highlight swift %}
protocol Identifiable {
    var name: String { get set }
}

class Car: Identifiable {
    var name: String
    init(name: String) { self.name = name }
}

class Street: Identifiable {
    var name: String
    init(name: String) { self.name = name }
}

var arr = [Identifiable]()

arr.append(Car(name: "Bentley"))
arr.append(Street(name: "First Street"))

{% endhighlight %}
