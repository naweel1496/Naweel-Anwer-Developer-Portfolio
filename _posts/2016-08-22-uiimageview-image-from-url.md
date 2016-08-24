---
layout: post
title: UIImageView extension to load image from URL
category: Swift
---

Here is a simple `UIImageView` extension to load image from URL

## Paramaters

- **url**: `NSURL` <br>Location of remote image

- **placeHolder**: `UIImage?` = nil <br>Image to be set if remote image is not available

- **completionHandler**: `(success: Bool) -> ())?` = nil <br>Optional handler invoked after the image is set

## Extension
{% highlight swift %}
extension UIImageView {
    func setImageFromURL(
        url: NSURL,
        placeHolder: UIImage? = nil,
        completion: ((success: Bool) -> ())? = nil ) {

        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)) {
            if let imageData: NSData = NSData(contentsOfURL: url) {
                let newImage = UIImage(data: imageData)
                dispatch_async(dispatch_get_main_queue()) {
                    self.image = newImage
                    completion?(success: true)
                }
            } else {
                dispatch_async(dispatch_get_main_queue()) {
                    self.image = placeHolder
                    completion?(success: false)
                }
            }
        }
    }
}

{% endhighlight %}