---
layout: post
title: Equatable enums in Swift
category: Swift
---

Equating enums in swift for simple cases like this one is pretty straight forward.

{% highlight swift %}
enum Vehicle {
    case Car, Bike
}

let v1 = Vehicle1.Car
let v2 = Vehicle1.Bike

v1 == v2 // False
{% endhighlight %}

But things get complicated, when the enum matures to something like this. Here you cannot use `==` operator directly.

{% highlight swift %}
enum Vehicle {
    enum CarType {
        case Sedan, SUV, MUV, HatchBack
    }
    enum BikeType {
        case Sports, Cruiser, Dirt
    }

    case Car(CarType)
    case Bike(BikeType)
    case Other(String)
}

{% endhighlight %}

So to equate enum like this we have two options

- Use the complicated nested switch casing
- or Implement the  [Equatable](https://developer.apple.com/library/watchos/documentation/Swift/Reference/Swift_Equatable_Protocol/index.html#//apple_ref/swift/intf/s:PSs9Equatable) protocol.

But using the nested switch casing has clear drawbacks. Hence we implement the Equatable protocol as we usually do for Classes.


{% highlight swift %}
// Conform to Equatable protocol
extension Vehicle: Equatable {}

func ==(lhs: Vehicle, rhs: Vehicle) -> Bool {
    switch (lhs, rhs) {
    case (.Car(let a), .Car(let b)):
        return a == b
    case (.Bike(let a), .Bike(let b)):
        return a == b
    case let (.Other(a), .Other(b)): // One let can also be used instead of multiple let
        return a == b
    default: return false
    }
}
{% endhighlight %}

After defining the `==` function we can **equate** our enums.

{% highlight swift %}
Vehicle.Car(.Sedan)      == Vehicle.Car(.Sedan)      // true
Vehicle.Car(.Sedan)      == Vehicle.Car(.MUV)        // false
Vehicle.Bike(.Sports)    == Vehicle.Car(.Sedan)      // false
Vehicle.Bike(.Sports)    == Vehicle.Bike(.Sports)    // true
Vehicle.Other("tractor") == Vehicle.Car(.HatchBack)  // false
Vehicle.Other("Bus")     == Vehicle.Car(.HatchBack)  // false
Vehicle.Other("tractor") == Vehicle.Other("tractor") // true
Vehicle.Other("tractor") == Vehicle.Other("crane")   // false

{% endhighlight %}
Our enum comparison has now clarity and brevity. And most important it's readable

For more information on comparison protocol you refer to [this](http://nshipster.com/swift-comparison-protocols/) post written by [Matt Thompson](http://nshipster.com/authors/mattt-thompson/) on NSHipster.

