# select不能用于ul

即，`select`无法用于，非`select`的`option`下拉选项列表

`select`只能用于

```html
<select>
    <option>
```
才可以。其他的元素，比如之前遇到的：

[【已解决】Selenium如何点击下拉框并选择某个值](http://www.crifan.com/selenium_click_dropdown_show_option_list_to_choose_someone)

中的

```html
<ul>
    <li role="option">
```

是用不了的。

所以最后就是用普通的，去`ul`下找到`li`的列表，通过index获得对应的元素，然后再去操作。

相关代码如下：

```python
cartNumOptionElemList = driver.find_elements_by_xpath('//ul[@class="dropdown-menu"]/li[@role="option"]')
cartNumOptionCount = len(cartNumOptionElemList)
logging.info("cartNumOptionElemList=%s,cartNumOptionCount=%s", cartNumOptionElemList, cartNumOptionCount)
if cartNumOptionCount < gCfg["msStore"]["onceBuyNum"]:
    logging.error("Current Cart select max number %s < expected select number %s", cartNumOptionCount, gCfg["msStore"]["onceBuyNum"])
    driver.quit()
toSelectIdx = gCfg["msStore"]["onceBuyNum"] - 1
# carNumSelect = Select(cartNumOptionElemList)
# carNumSelect.select_by_index(gCfg["msStore"]["onceBuyNum"])
carNumSelectElem = cartNumOptionElemList[toSelectIdx]
logging.info("carNumSelectElem=%s", carNumSelectElem)
carNumSelectElem.click()
# aLinkElem = carNumSelectElem.find_element_by_link_text(str(gCfg["msStore"]["onceBuyNum"]))
# logging.info("aLinkElem=%s", aLinkElem)
# aLinkElem.click()
```
