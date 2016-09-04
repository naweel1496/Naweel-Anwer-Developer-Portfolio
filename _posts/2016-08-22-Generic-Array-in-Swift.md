---
layout: post
title: More flexible arrays in Swift
category: Swift
---

There comes a time when you have to create an Array of objects which are  of different types. A generic solution to this problem is to create an `Array<AnyObject>`

## Array\<AnyObject>
Array<AnyObject> can accommodate almost everything into it. But wait..

Why do you need it?

Whenever there comes a need to create an array of anyobject, just consider redesigning the code instead. Why would you create a list of heterogenous type in the first place?

But if the list is somewhat similar then you can use Protocol oriented Programming for this.

## Protocol Oriented Solution
Swift is focusing more on protocol oriented programming. So if you have to create an array of **similar** but not the same data types, then you can make all the similar types conform to a `Protocol` and create an array of the Protocol.

Here is the example
{% highlight swift %}
protocol Shape {
    var color: String { get set}
    func area() -> Double
}

struct Circle: Shape {
    var color: String
    var radius: Double
    func area() -> Double {
        return radius * radius * M_PI
    }
}

struct Square: Shape {
    var color: String
    var sideLength: Double
    func area() -> Double {
        return sideLength * sideLength
    }
}

var arr = [Shape]()
arr.append(Circle(color: "Red", radius: 10.0))
arr.append(Square(color: "Green", sideLength: 50))

{% endhighlight %}
