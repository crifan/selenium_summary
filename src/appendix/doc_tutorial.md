# Selenium文档

## 官网文档

* 官网
  * 英文
    * 3 Navigating — Selenium Python Bindings 2 documentation
      * https://selenium-python.readthedocs.io/navigating.html
    * 4 Locating Elements — Selenium Python Bindings 2 documentation
      * https://selenium-python.readthedocs.io/locating-elements.html
    * 5 Waits — Selenium Python Bindings 2 documentation
      * https://selenium-python.readthedocs.io/waits.html
    * 6 Page Objects — Selenium Python Bindings 2 documentation
      * https://selenium-python.readthedocs.io/page-objects.html
    * 7 WebDriver API — Selenium Python Bindings 2 documentation
      * https://selenium-python.readthedocs.io/api.html
  * 中文
    * 4 查找元素 — Selenium-Python中文文档 2 documentation
      * https://selenium-python-zh.readthedocs.io/en/latest/locating-elements.html
    * 5 等待页面加载完成(Waits) — Selenium-Python中文文档 2 documentation
      * https://selenium-python-zh.readthedocs.io/en/latest/waits.html
    * 6 页面对象 — Selenium-Python中文文档 2 documentation
      * https://selenium-python-zh.readthedocs.io/en/latest/page-objects.html
    * 7 WebDriver API — Selenium-Python中文文档 2 documentation
      * https://selenium-python-zh.readthedocs.io/en/latest/api.html

## WebElement有很多函数和属性

整理如下，供有个概念：

* 函数
  * `clear()`
  * `click()`
  * `find_element(by='id', value=None)`
  * `find_element_by_class_name(name)`
  * `find_element_by_css_selector(css_selector)`
  * `find_element_by_id(id_)`
  * `find_element_by_link_text(link_text)`
  * `find_element_by_name(name)`
  * `find_element_by_partial_link_text(link_text)`
  * `find_element_by_tag_name(name)`
  * `find_element_by_xpath(xpath)`
  * `find_elements(by='id', value=None)`
  * `find_elements_by_class_name(name)`
  * `find_elements_by_css_selector(css_selector)`
  * `find_elements_by_id(id_)`
  * `find_elements_by_link_text(link_text)`
  * `find_elements_by_name(name)`
  * `find_elements_by_partial_link_text(link_text)`
  * `find_elements_by_tag_name(name)`
  * `find_elements_by_xpath(xpath)`
  * `get_attribute(name)`
  * `get_property(name)`
  * `is_displayed()`
  * `is_enabled()`
  * `is_selected()`
  * `screenshot(filename)`
  * `send_keys(*value)`
  * `submit()`
  * `value_of_css_property(property_name)`
* 属性
  * `id`
  * `location`
  * `parent`
  * `rect`
  * `screenshot_as_png`
  * `size`
  * `text`
  * `tag_name`

更多内容详见官网文档：[WebElement](http://selenium-python.readthedocs.io/api.html#module-selenium.webdriver.remote.webelement)

其中：
* `find_element_by_link_text`
* `find_element_by_partial_link_text`

指的是标签`a`的`link`，而其他标签是用不了的。
