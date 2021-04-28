# 触发搜索

对于想要触发百度首页中的搜索来说，除了**点击元素**外，还可以**模拟输入回车键**。

* 触发百度搜索
  * 方式1：点击`百度一下`按钮
    ```python
    BaiduSearchId = "su"
    baiduSearchButtonElem = chromeDriver.find_element_by_id(BaiduSearchId)
    baiduSearchButtonElem.click()
    ```
  * 方式2：模拟输入`回车键`
    ```python
    from selenium.webdriver.common.keys import Keys
    # Method 1: emulate press Enter key
    searchButtonElem.send_keys(Keys.RETURN)
    ```

附上：模拟百度输入并搜索的相关代码

```python
searchStr = "crifan"
searchButtonElem.send_keys(searchStr)
print("Entered %s to search box" % searchStr)

# click button
# Method 1: emulate press Enter key
# searchButtonElem.send_keys(Keys.RETURN)
# print("Pressed Enter/Return key")

# Method 2: find button and click
BaiduSearchId = "su"
baiduSearchButtonElem = chromeDriver.find_element_by_id(BaiduSearchId)
print("baiduSearchButtonElem=%s" % baiduSearchButtonElem)
baiduSearchButtonElem.click()
print("Clicked button %s" % baiduSearchButtonElem)
```
