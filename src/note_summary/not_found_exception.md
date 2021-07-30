# 找不到元素会抛异常

Selenium的`find_element_by_xpath`，是找单个元素，如果找不到，则会抛异常`NoSuchElementException`

->和常见的逻辑，找不到只返回空`None`，不一样

-》代码中要注意，根据你的需要，可能需要捕获异常

举例：

```python
for curIdx, eachNormalLi in enumerate(normalLiList):
    try:
        descItem = eachNormalLi.find_element_by_xpath(".//div[@class='b_caption']/p")
    except:
        logging.error("Failed to find description(b_caption) element")
        continue
```

而对应的，找多个元素，返回列表的`find_elements_by_xpath`，则不会排除异常，如果找不到，则返回空列表`[]`而已

总结：

* 找单个元素的 [find_element_by_xpath](https://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.find_element_by_xpath)
  * 如果找不到，会抛出异常`NoSuchElementException`
    * 你需要根据你的情况决定，是否要捕获异常
  * 对应官网解释
    > find_element_by_xpath(xpath)
    > 
    > Finds an element by xpath.
    > 
    > Args:
    >   * xpath - The xpath locator of the element to find.
    > 
    > Returns:
    >   * WebElement - the element if it was found
    > 
    > Raises::
    >   * NoSuchElementException - if the element wasn’t found
    > 
    > Usage:
    > 
    > element = driver.find_element_by_xpath(‘//div/td[1]’)
* 找多个元素的 [find_elements_by_xpath](https://selenium-python.readthedocs.io/api.html#selenium.webdriver.remote.webdriver.WebDriver.find_elements_by_xpath)
  * 如果找不到，只是返回空列表，不会抛异常 -》 无需捕获异常
  * 对应官网解释
    > find_elements_by_xpath(xpath)
    > 
    > Finds multiple elements by xpath.
    > 
    > Args:
    >   * xpath - The xpath locator of the elements to be found.
    > 
    > Returns:
    >   * list of WebElement - a list with elements if any was found. An empty list if not
    > 
    > Usage:
    > 
    > elements = driver.find_elements_by_xpath(“//div[contains(@class, ‘foo’)]”)
