# 偶尔刷新后才能找到元素

即：有时候点击按钮后页面刷新且url地址也换了，再去用driver寻找元素之前，先要refresh然后才能找到

但是有时候却又不需要refresh也可以

最后是：

```python
driver.refresh()
inputEmailElement = driver.find_element_by_xpath('//div[@class="placeholderContainer"]/input[@name="loginfmt"]’)
```

或：

```python
inputEmailElement = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.XPATH, '//div[@class="placeholderContainer"]/input[@name="loginfmt"]')))
```

好像都可以。

注：

不过还是不知道为何前面的代码：

```python
placeholderElement = driver.find_element_by_xpath('//div[@class="phholder"]/div[@class="placeholder"]')
placeholderElement = WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.XPATH, '//div[@class="phholder"]/div[@class="placeholder"]')))
placeholderElement = driver.find_element_by_xpath('//div[@class="phholder"]')
phholderElement = driver.find_element_by_class_name('phholder')
logging.info("phholderElement=%s", phholderElement)
placeholderElement = phholderElement.find_element_by_class_name("placeholder")
```

此处已确保`xpath`写的是对的，且查看页面元素的确是存在的，但却还是找不到元素。
