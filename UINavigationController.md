### Push 实现类似Present效果 

```swift
let transition = CATransition()
transition.duration = 0.3
transition.timingFunction = CAMediaTimingFunction(name: .easeInEaseOut)
transition.type = .fade
navigationController?.view.layer.add(transition, forKey: nil)
```
