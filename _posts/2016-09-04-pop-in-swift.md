---
layout: post
title: Understanding Protocol Oriented programming in Swift
category: Swift
---

WWDC2015 was all about `Protocol oriented programming`. How is it different?

Lets see.

## Inheritance
Inheritance is widely used and loved by lot. But people have started talking against Inheritance

Consider a simple example:
{% highlight swift %}
class Shape {
    var color: String!
    func area() -> Double {
        fatalError("This method is abstract & must be overridden before using")
    }
}

class Circle: Shape {
    var radius: Double! = 10.4
    override func area() -> Double {
        return radius * radius * M_PI
    }
}

class Square: Shape {
    var sideLength: Double! = 10.0
    override func area() -> Double {
        return sideLength * sideLength
    }
}
{% endhighlight %}


## Protocol Oriented Solution
Lets reimplement above code using Protocols

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


### Benefits of protocol oriented code

#### Code reuse in Value types
One of the basic difference between `Class` and `struct` is that classes can inherit while  structs cannot. Swift clearly is promoting value type over reference type. So protocols can be used to make your code more reusable in Value-type environment.

#### Clarity
The structures in above example more clearly state their properties and methods. There is no hidden property/method. 

But if you conform to a lot of protocols, it makes your class definition very long. But you could always use [Object composition][]

#### Conform to multiple protocols
One of the drawbacks of inheritance is there cannot be multiple superclasses(This design is discouraged although). But on the contrary a Struct/Class can conform to multiple protocols

[Object composition]: https://en.wikipedia.org/wiki/Object_composition