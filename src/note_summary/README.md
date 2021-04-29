# Selenium心得和总结


## 单个WebElement本身好像不支持截图

详见：

[WebElement.screenshot(filename)](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webelement.WebElement.screenshot)

和：

[WebElement.screenshot_as_png()](http://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webelement.WebElement.screenshot_as_png)

以为单个WebElement也不支持截图，但是试了试：

```python
multipleXpathRule = '//div/......'
priceSpanElement = driver.find_element_by_xpath(multipleXpathRule)
priceSpanElement.screenshot("priceElement.png")
```

结果报错：

`selenium.common.exceptions.WebDriverException: Message: unknown command: session/7160497aa2d4dc2029bcb5c4d2e8045a/element/0.07853595638566757-1/screenshot`

所以算了，不去管这个了。感觉是**单个WebElement本身好像不支持截图**

## get的url没法back或forward，而navigate的url可以
详见：
[URL Loading in Selenium Webdriver: All about get() and navigate() – Make Selenium Easy](http://makeseleniumeasy.com/2017/05/04/url-loading-in-selenium-webdriver-all-about-get-and-navigate/)
