### 修改`UIAlertController`按钮颜色

```swift
let alert = UIAlertController(...)
present(alert, animated: true, completion: nil)
alert.view.tintColor = .red
```

如果要全局修改按钮颜色，可以在AppDelegate中设置

```swift
UIView.appearance(whenContainedInInstancesOf: [UIAlertController.self]).tintColor = .red
```

### 修改message的对齐方式

默认`UIAlertController`中的 title与message文本的对齐方式是居中对齐。

```swift
let alert = UIAlertController(title: "提示", message: "", preferredStyle: .alert)
alert.addAction(UIAlertAction(title: "确定", style: .cancel, handler: { _ in

}))
        
let paragraph = NSMutableParagraphStyle()
paragraph.alignment = .left
let message = NSAttributedString(string: "这是AlertController的Message部分，靠左对齐",
                                 attributes: [.font : UIFont.systemFont(ofSize: 15),
                                              .paragraphStyle: paragraph])
alert.setValue(message, forKey: "attributedMessage")
present(alert, animated: true, completion: nil)
```

### 修改`title` 与 `message` 之间的间距
