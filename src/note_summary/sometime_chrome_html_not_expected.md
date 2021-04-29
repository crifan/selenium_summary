# 偶尔Chrome右键元素不是你要的

即：有时候Chrome中直接右键找到的元素，并不一定是你想要的

比如：

![chrome右键输入账号](../assets/img/chrome_right_click_input_box.png)

是个：

```html
<div class="placeholder">
```

但是其实此处要找的是 **可以允许输入的input输入框**

而后来是无意间自己调试，从中间的区域，右键后：

![Sign in去右键](../assets/img/signin_right_click.png)

然后一点点点击看子元素：

![一点点去看子元素](../assets/img/one_by_one_see_child_element.png)

最后找到真正的input的：

![找到真正的input元素](../assets/img/found_real_input_element.png)

相关代码是：

```html
<input type="email" name="loginfmt" id="i0116" ......
                attr: inputAttributes" aria-label="Enter your email, phone, or Skype.">
```
