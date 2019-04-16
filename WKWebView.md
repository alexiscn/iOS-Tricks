
### 原生方式查看WebView图片

JavaScript端遍历所有的图片，重写点击事件，点击图片时设置特殊scheme的跳转。原生端捕获URL跳转事件，判断特殊的scheme，解析URL，用原生的方式展示图片。

```js
var images = document.getElementsByTagName('img');
for (var i = 0; i < images.length; i ++) {
    var img = images[i];
    var src = img.src;
    img.onclick = (function(urlString) {
        return function() {
            var encodedURI = encodeURIComponent(urlString)
            location.href = "nativeProtocol://" + encodedURI
        }
    })(src)
}
```
由于JavaScript需要在DOM加载完成后才有效果，所有就在WKWebView的 didFinish navigation中注入一次就好。

```swift
func webView(_ webView: WKWebView, didFinish navigation: WKNavigation!) {
    let jsCode = ... // read from file or in code
    webView.evaluateJavaScript(jsCode, completionHandler: nil)
}
```

点击图片的时候会触发

```swift
func webView(_ webView: WKWebView, decidePolicyFor navigationAction: WKNavigationAction, decisionHandler: @escaping (WKNavigationActionPolicy) -> Void) {
    if let url = navigationAction.request.url, url.scheme == "nativeProtocol" {
            let src = url.absoluteString.replacingOccurrences(of: "nativeProtocol://", with: "")
            if let url = src.removingPercentEncoding {
                // get image url
            }
    }
}
```

获得图片的URL就可以用原生方式在展示了