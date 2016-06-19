---
layout: post
title: Tryouts of reduce function in Swift
category: Swift
---

Swift has a set of awesome high order functions like `map`, `filter` and `reduce`. Although reduce is relatively complex, it has immense `flexibility` and `power`. Reduce has flexibility to such an extent that it can do all possible array operations.

## Array methods re implemented using reduce
You can check out some of the array functionalities that I have re implemented using reduce

#### array.count
{% highlight swift %}
let totalElements = ["A", "B", "C", "D", "E"].reduce(0) { $0.0 + 1}
// Returns 5
{% endhighlight %}

#### array.insertElement(atIndex)
{% highlight swift %}
let newElement = "NEW"; let atIndex = 3
let newList: [String] = ["A", "B", "C", "D", "E"].reduce([String]()) { (accum, char) in
    if accum.count == atIndex {
        return accum + [newElement, char]
    }
    return accum + [char]
}
// Returns ["A", "B", "C", "NEW", "D", "E"]
{% endhighlight %}

#### array.last
{% highlight swift %}
let chars = ["A", "B", "C", "D", "E"]
let lastElement: String = chars.reduce(chars[0]) { (_, char) in
    return char
}
// Returns "E"
{% endhighlight %}

## map using reduce
If this wasnt impressive enough, check out how `map` can be implemented using reduce.

{% highlight swift %}

let stringedNums = [1, 2, 3, 4].map { String( $0) }

// reduce implementation of above map
let stringedNums = [1, 2, 3, 4].reduce([String]()) { (accum, num) in
    return accum + [String(num)]
}
// Returns ["1", "2", "3", "4"]
{% endhighlight %}

---

## filter using reduce
Similarly `filter` implementation is

{% highlight swift %}
// Filters odd numbers from array
[1, 2, 3, 4, 5].filter {
    $0 % 2 == 0
}

// reduce equivalent of above filter
[1, 2, 3, 4, 5].reduce([Int]()) { (accum, num) in
    return num % 2 == 0 ? accum + [num] : accum
}
// Returns [2, 4]
{% endhighlight %}

---

## Now what ?

reduce can be used to implement native array methods. It can also be used as map and filter. But what was the point ?

Point was to show how powerful reduce function is. It happens that we unknowingly chain map and filter as requirement changes. This chaining becomes cumbersome. If you have very specific requirements you can always use reduce. You get the desired outcome in one array traversal.
