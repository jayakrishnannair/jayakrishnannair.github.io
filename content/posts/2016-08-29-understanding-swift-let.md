---
title: 'Understanding Swift: let'
author: jayakrishnan
type: post
date: 2016-08-29T17:50:48+00:00
url: /2016/08/29/understanding-swift-let/
categories:
  - Notes to Self
  - Swift

---
Here is the handler code for a slider in XCode 7

    @IBAction func handleSlider(sender: UISlider) {
        var value = sender.value
        print("value \(value) ")
    }


If you type in this code, XCode will issue the following warning near the declaration of the _var value_, _Variable &#8216;value&#8217; was never mutated; consider changing to &#8216;let&#8217; constant._ Once you choose that option, the code changes to this and the warning disappears.

    @IBAction func handleSlider(sender: UISlider) {
        let value = sender.value
        print("value \(value) ")
    }


Using _let_ instead of _var_ conveys that the variable is immutable. The value is set once and never changed. If you are reading someone else&#8217;s code and encounter _let_, you can be assured that the value of this variable is not changing in the code.

This works for collection classes and arrays as well.  If you use _let_ before an array or dictionary, then you cannot add or remove contents from it.

For example here is a piece of code that will give an error because _someInts_ is declared as immutable

    let someInts = [Int]()
    someInts.append(3)


The same is true in this case as well

    let namesOfIntegers = [Int:String]()
    namesOfIntegers[16] = "sixteen"
