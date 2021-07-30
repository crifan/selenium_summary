# 模拟bing必应搜索

此处用Selenium（的Chrome）模拟：

* 打开 bing必应搜索
  * https://cn.bing.com/
* 输入文字
* 点击按钮触发搜索
* 从第一页搜索结果中，解析出搜索结果
  * 标题`title`
  * 网址`url`
  * 日期`date`
  * 描述`description`

## 调试页面

调试期间的相关页面：

* 打开bing主页
  * 页面
    * ![selenium_bing_open_home](../assets/img/selenium_bing_open_home.png)
* 输入框：输入文字
  * html
    ```html
    <input class="b_searchbox" id="sb_form_q" name="q" title="输入搜索词" type="search" value="" maxlength="100" autocapitalize="off" autocorrect="off" autocomplete="off" spellcheck="false" aria-controls="sw_as">
    ```
  * 页面
    * ![selenium_bing_input_box](../assets/img/selenium_bing_input_box.png)
    * ![selenium_bing_inputed_str](../assets/img/selenium_bing_inputed_str.png)
* 点击：搜索按钮
  * html
    ```html
    <input type="submit" class="b_searchboxSubmit" id="sb_form_go" tabindex="0" name="go">
    ```
  * 页面
    * ![selenium_bing_search_button](../assets/img/selenium_bing_search_button.png)
* 搜索结果
  * 中间的搜索结果
    * 列表
      * 页面
        * ![selenium_bing_result_ol_list](../assets/img/selenium_bing_result_ol_list.png)
    * 每条搜索结果
      * 页面
        * ![selenium_bing_search_result_top](../assets/img/selenium_bing_search_result_top.png)
        * ![selenium_bing_search_result_bottom](../assets/img/selenium_bing_search_result_bottom.png)
      * 普通结果
        * html
          ```html
              <li class="b_algo">
                  <h2><a target="_blank" href="http://www.drv5.cn/azgame/77154.html"
                          h="ID=SERP,5143.1"><strong>白夜琉璃</strong>手游下载-<strong>白夜琉璃</strong>手游内测版v1.4.8-第五驱动</a></h2>
                  <div class="b_caption">
                      <div class="b_attribution" u="0|5124|4545703417479742|AOP9gfi8m1gTJYYm89LkD12SrZYxtwiM">
                          <cite>www.drv5.cn/azgame/77154.html</cite><span class="c_tlbxTrg"><span class="c_tlbxH"
                                  h="BASE:CACHEDPAGEDEFAULT" k="SERP,5144.1"></span></span></div>
                      <p>2021-5-11 · 白夜琉璃是一款浪漫情缘<strong>题材</strong>的唯美仙侠<strong>游戏</strong>在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界，
                          。</p>
                  </div>
              </li>
              <li class="b_algo">
                  <h2><a target="_blank" href="https://www.lanrentuku.com/shouyou/47585.html"
                          h="ID=SERP,5160.1"><strong>白夜琉璃</strong>手游下载-<strong>白夜琉璃</strong>手游手机安卓版v1.4.8-懒人下载</a></h2>
                  <div class="b_caption">
                      <div class="b_attribution" u="1|5058|4544492236377359|iCr1uUVRGmUSmPG2Qas_VurCNnMh9v9I">
                          <cite>https://www.lanrentuku.com/shouyou/47585.html</cite><span class="c_tlbxTrg"><span class="c_tlbxH"
                                  h="BASE:CACHEDPAGEDEFAULT" k="SERP,5161.1"></span></span></div>
                      <p>2021-5-11 · <strong>白夜琉璃</strong>是一款浪漫情缘<strong>题材</strong>的唯美仙侠<strong>游戏</strong>在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验，
                          。</p>
                  </div>
              </li>
          ```
      * 之前有：顶部和底部带广告
        * 顶部广告
          * 页面
            * ![selenium_bing_result_ad_top](../assets/img/selenium_bing_result_ad_top.png)
          * html
            ```html
                <li class="b_ad">
                    <ul>
                        <li class="b_adLastChild">
                            <div class="sb_add sb_adTA">
                                <h2><a id="tile_link_cn" target="_blank" class=" b_restorableLink"
                                        onmousedown="ad_pt_mousedown_cn(this)" onmouseup="ad_pt_mouseup_cn(this)"
                                        href="http://e.so.com/search/eclk?p=dac8DLoMp5KV6LLF4qKf_LLuqlgwadNTcdmVwLMv6rJu6AEsht7C_darl2_QXquzKxu0sJtliKThz1xVpI8DRTMcm5djUgKARzVcTToe5bHpa-jCy3BuA7arrxd641N3fJB6PThDEBq0U5VGAk502OHWwE4XHTap6_FZszlE2SpV8BP8-VUJahRWYxcPOASP_O158ojqdBncS4QMzSW6F3bFmSPtjq_D-2WY1EjdTIWJktETB_Oi5GWHQKA1yJilQFMZVhQmsmshEOyTRHUkU5-YXR9dAoHhD-Y4iDUGdNKQNpa8LGBIiD97Iw75ekuWE79cYm0F4mMvB2Cg4xiNTKYAX3sVtILG3STUtVRzySKCu0xwUDbXB-_u0x2KiUzXcDZD1ymgU0p5EK2l2TSi5yamarcfRrpMF9eKP_L-S2ENmns4BP5DlEN0S_XQ_vlbG8To_6ssqiEKdJmGj0JVm8iGlut8fEfcEA8DA0ZxVw0We1_kulRatXYapd64MmShssGx__K5GNZeGpfhJaZhWzd7j26QJi5kBblTut9oIJhJ0vtOtaGvC4zKiw1MwayTxbh32OpuXhnxkghgaqKzj5hzyHsXfhVHtBp5RpIld_ZEbz5jlILD2vlSBsAiiA15GYdrStSqJfF-l4IKhNcg9sq27zlCzQGc9Sv3of_R9tE-vCtM5vYEUYUmbXxjtxCBdn0-Uy7NDTkgqfBEdBxOtvzKofGd897G02A5j2HDLgeCV37kew&amp;ns=0&amp;v=2&amp;at=AeeZveWknOeQieeSg-a4uOaIjwJfMjAyMQHnmb3lpJznkInnkoMC55S16ISR54mIX-eCueWHu-i_m-WFpQHmuLjmiI8C&amp;aurl=aHR0cDovL2x1Y2suc25nODg5LmNvbS9vbi95eC1zeS94aWFueGlhNDEvczUvY2NpZDAyNjgv&amp;sig=09e3&amp;bt=1"
                                        h="ID=SERP,5397.1,Ads"><strong>白夜琉璃游戏</strong>_2021<strong>白夜琉璃</strong>电脑版_点击进入<strong>游戏</strong></a>
                                </h2>
                                <div class="b_caption">
                                    <div class="b_attribution"><cite>luck.sng889.com</cite></div>
                                    <p class=""><span class="b_adProvider">来自
                                            360</span>2021免费仙侠<strong>游戏</strong>「<strong>白夜琉璃</strong>」,全新地图,爆率升级!结婚组队,自由PK!「<strong>白夜琉璃</strong>」今日新服开启,注册送首充,送VIP!<span
                                            class="b_adSlug b_opttxt b_divdef">广告</span></p>
                                </div>
                                <div class="ad_fls">
                                    <p class="b_ads1line b_secondaryText"><strong>游戏排行:</strong> <a id="tile_link_cn"
                                            target="_blank" onmousedown="ad_pt_mousedown_cn(this)"
                                            onmouseup="ad_pt_mouseup_cn(this)"
                                            ..........
                                    <p class="b_ads1line b_secondaryText"><strong>游戏入口:</strong> <a id="tile_link_cn"
                                            target="_blank" onmousedown="ad_pt_mousedown_cn(this)"
                                            onmouseup="ad_pt_mouseup_cn(this)"
                                            ...
                                            h="ID=SERP,5408.1,Ads">火爆开服</a> · <a id="tile_link_cn" target="_blank"
                                            onmousedown="ad_pt_mousedown_cn(this)" onmouseup="ad_pt_mouseup_cn(this)"
                                            href="http://e.so.com/search/eclk?p=fd2e_lUflvr7T14kFM2Y4HAwiDR081-etamo5kC7tCZsMSq3lK6DVTx2mavdL42PW3TtsLBhlhvEp10HeCrKp1qQPrHKt063VUoDaD-0mdYFNxsh2kZy3Mtu5UxABBnnfe7dIJfmX4x9yI7gCyQR9kS6ZKfSsSgDrqDowDtyf9RuPQfVi74wRa-kFRfp0Mj20tkU2Au43FrjVtD6M4jgJebZ9iliM0dgTNsIwIY2VMRmwGhp-CK0dOC_7SdKeo67Py660YMr-wPzBcho0XXqq9jO3cOPh6zelyyhws5c3xKz-JpKJKYlwQzrQqArpfmVOJ-7UqaHOqoPeynSJ4D4ZSRqd8c8H6LPESEeP7qP-IhWlfqJmxN3iiAeXEkXyGbag86aMdPc1MC8Ckdr0Vj9Ny7UnPASL9a50eOYR8JRTTi8LWlRvqKk6EsxErTwDSZNPzOXCEQTygYkPq3ieWF5Mlo1DSdj2x07L1c3AgmgunyI79lN448EmEyGjhJUlsd7QSYEFCu7opv6Ls-icvVK2mQB-zr7mXrc43_W_5TaKSRQvSrF1MAZOsPB6_xkcBhqc6znuyfKmg6Rr7pZPtO-_UcftzLeJqZKBFV5X_bjBebuyduC7-s7Z0rY1dfkCvMPEcpgOQT2BgUkGf0ctfLhWAGQ-tg4s5azIY8GdJSzVgpNIIvjEK1nFk2eF48-wO4c1NeE7T1HYF71eymozl4bMEoGDEPiFS-i4075LW4TIN1shl_DnA&amp;ns=0&amp;v=2&amp;at=AeeZveWknOeQieeSg-a4uOaIjwJfMjAyMQHnmb3lpJznkInnkoMC55S16ISR54mIX-eCueWHu-i_m-WFpQHmuLjmiI8C&amp;aurl=aHR0cDovL2x1Y2suc25nODg5LmNvbS9vbi95eC1zeS94aWFueGlhNDEvczUvc3QtcnBnLw&amp;sig=23ba&amp;bt=1&amp;posid=220202&amp;positionType=1"
                                            h="ID=SERP,5409.1,Ads">注册入口</a></p>
                                </div>
                            </div>
                        </li>
                    </ul>
                </li>
            ```
        * 底部广告
          * 页面
            * ![selenium_bing_result_ad_bottom](../assets/img/selenium_bing_result_ad_bottom.png)
          * html
              ```html
                  <li class="b_ad b_adBottom">
                      <ul>
                          <li class="b_adLastChild">
                              <div class="sb_add sb_adTA">
                                  <h2><a id="tile_link_cn" target="_blank" class=" b_restorableLink"
                                          onmousedown="ad_pt_mousedown_cn(this)" onmouseup="ad_pt_mouseup_cn(this)"
                                          href="http://e.so.com/search/eclk?p=dac8DLoMp5KV6LLF4qKf_LLuqlgwadNTcdmVwLMv6rJu6AEsht7C_darl2_QXquzKxu0sJtliKThz1xVpI8DRTMcm5djUgKARzVcTToe5bHpa-jCy3BuA7arrxd641N3fJB6PThDEBq0U5VGAk502OHWwE4XHTap6_FZszlE2SpV8BP8-VUJahRWYxcPOASP_O158ojqdBncS4QMzSW6F3bFmSPtjq_D-2WY1EjdTIWJktETB_Oi5GWHQKA1yJilQFMZVhQmsmshEOyTRHUkU5-YXR9dAoHhD-Y4iDUGdNKQNpa8LGBIiD97Iw75ekuWE79cYm0F4mMvB2Cg4xiNTKYAX3sVtILG3STUtVRzySKCu0xwUDbXB-_u0x2KiUzXcDZD1ymgU0p5EK2l2TSi5yamarcfRrpMF9eKP_L-S2ENmns4BP5DlEN0S_XQ_vlbG8To_6ssqiEKdJmGj0JVm8iGlut8fEfcEA8DA0ZxVw0We1_kulRatXYapd64MmShssGx__K5GNZeGpfhJaZhWzd7j26QJi5kBblTut9oIJhJ0vtOtaGvC4zKiw1MwayTxbh32OpuXhnxkghgaqKzj5hzyHsXfhVHtBp5RpIld_ZEbz5jlILD2vlSBsAiiA15GYdrStSqJfF-l4IKhNcg9sq27zlCzQGc9Sv3of_R9tE-vCtM5vYEUYUmbXxjtxCBdn0-Uy7NDTkgqfBEdBxOtvzKofGd897G02A5j2HDLgeCV37kew&amp;ns=0&amp;v=2&amp;at=AeeZveWknOeQieeSg-a4uOaIjwJfMjAyMQHnmb3lpJznkInnkoMC55S16ISR54mIX-eCueWHu-i_m-WFpQHmuLjmiI8C&amp;aurl=aHR0cDovL2x1Y2suc25nODg5LmNvbS9vbi95eC1zeS94aWFueGlhNDEvczUvY2NpZDAyNjgv&amp;sig=09e3&amp;bt=1"
                                          h="ID=SERP,5412.1,Ads"><strong>白夜琉璃游戏</strong>_2021<strong>白夜琉璃</strong>电脑版_点击进入<strong>游戏</strong></a>
                                  </h2>
                                  <div class="b_caption">
                                      <div class="b_attribution"><cite>luck.sng889.com</cite></div>
                                      <p class=""><span class="b_adProvider">来自
                                              360</span>2021免费仙侠<strong>游戏</strong>「<strong>白夜琉璃</strong>」,全新地图,爆率升级!结婚组队,自由PK!「<strong>白夜琉璃</strong>」今日新服开启,注册送首充,送VIP!<span
                                              class="b_adSlug b_opttxt b_divdef">广告</span></p>
                                  </div>
                              </div>
                          </li>
                      </ul>
                  </li>
              ```

## 代码

* 注
  * （写代码）之前还有（2个）ad广告结果，此处后续调试没出现。但此处代码已包含相关逻辑。
  * 最新全部代码详见
    * https://github.com/crifan/crifanLibPython/blob/master/python3/crifanLib/thirdParty/crifanSelenium.py

下面贴出对应代码：

### 模拟打开必应和触发必应搜索

```python
def getBingSearchResult(searchKeyword, driver=None):
    """
    Emulate bing search, return search result

    Args:
        searchKeyword (str): str to search
        driver (WebDriver): selenium web driver. Default is None. If None, create a new one.
    Returns:
        result dict list
    Raises:
    Examples:
        '游戏题材 白夜琉璃'
    """
    if not driver:
        driver = webdriver.Chrome()

    BingHomeUrl = "https://cn.bing.com/"
    # https://cn.bing.com/search?q=%e7%99%bd%e5%a4%9c%e4%bd%bf%e5%be%92&FORM=R5FD7

    searchResultDictList = []

    try:
        driver.get(BingHomeUrl)

        # <input class="b_searchbox" id="sb_form_q" name="q" title="输入搜索词" type="search" value="" maxlength="100" autocapitalize="off" autocorrect="off" autocomplete="off" spellcheck="false" aria-controls="sw_as">
        searchBoxId = "sb_form_q"
        searchBoxElem = driver.find_element_by_id(searchBoxId)
        logging.info("Found search box %s", searchBoxElem)

        searchBoxElem.send_keys(searchKeyword)
        logging.info("Inputed text %s", searchKeyword)

        # <input type="submit" class="b_searchboxSubmit" id="sb_form_go" tabindex="0" name="go">
        searchButtonId = "sb_form_go"
        searchButtonElem = driver.find_element_by_id(searchButtonId)
        searchButtonElem.click()
        logging.info("Clicked button %s to trigger seach", searchButtonElem)

        # wait bing search complete -> show some element
        # <span class="sb_count">9,120,000 条结果</span>
        MaxWaitSeconds = 10
        searchCountElem = WebDriverWait(driver, MaxWaitSeconds).until(
            EC.presence_of_element_located((By.XPATH, "//span[@class='sb_count']"))
        )
        logging.info("Search complete, showing: %s", searchCountElem)

        searchResultDictList = parseBingSearchResult(driver)
        searchResultNum = len(searchResultDictList)
        logging.info("Found %d search result", searchResultNum)
    except Exception as e:
        errStr = str(e)
        # 'Message: timeout: Timed out receiving message from renderer: 10.000\n  (Session info: chrome=92.0.4515.107)\n'
        logging.error("selenium open %s exception: %s", BingHomeUrl, errStr)

    return searchResultDictList
```

### 从必应搜索页面中提取搜索结果

其中包含了，从搜索结果页面中解析出相关信息：标题title、网址链接url、日期date、描述description

```python

def parseBingSearchResult(driver, isIncludeAd=True):
    """
    Parse bing search result from current (search result) page

    Args:
        driver (WebDriver): selenium web driver
        isIncludeAd (bool): return result is include ad part or not
    Returns:
        result dict list
    Raises:
    """
    searchResultDictList = []

    # <ol id="b_results">
    resultId = "b_results"

    # driver.find_element_by_xpath("//ol[@id='b_results']")

    resultElem = driver.find_element_by_id(resultId)
    logging.info("resultElem=%s", resultElem)
    if resultElem:

        # allLiXpath = "//li[@class='b_algo' or @starts-with(@class, 'b_ad')]"
        # allLiXpath = '//li[@class="b_algo" or starts-with(@class, "b_ad")]'
        # allLiXpath = "//li[@class='b_algo' or starts-with(@class, 'b_ad')]"
        # resultLiList = resultElem.find_elements_by_xpath(allLiXpath)
        # logging.info("resultLiList=%s", resultLiList)
        # resultLiNum = len(resultLiList)
        # logging.info("resultLiNum=%s", resultLiNum)

        normlLiXpath = ".//li[@class='b_algo']"
        normalLiList = resultElem.find_elements_by_xpath(normlLiXpath)
        normalLiNum = len(normalLiList)
        logging.info("normalLiNum=%s", normalLiNum)

        # normal result item
        """
            <li class="b_algo">
                <h2><a target="_blank" href="http://www.drv5.cn/azgame/77154.html"
                        h="ID=SERP,5143.1"><strong>白夜琉璃</strong>手游下载-<strong>白夜琉璃</strong>手游内测版v1.4.8-第五驱动</a></h2>
                <div class="b_caption">
                    <div class="b_attribution" u="0|5124|4545703417479742|AOP9gfi8m1gTJYYm89LkD12SrZYxtwiM">
                        <cite>www.drv5.cn/azgame/77154.html</cite><span class="c_tlbxTrg"><span class="c_tlbxH"
                                h="BASE:CACHEDPAGEDEFAULT" k="SERP,5144.1"></span></span></div>
                    <p>2021-5-11 · 白夜琉璃是一款浪漫情缘<strong>题材</strong>的唯美仙侠<strong>游戏</strong>在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界，
                        。</p>
                </div>
            </li>
            <li class="b_algo">
                <h2><a target="_blank" href="https://www.lanrentuku.com/shouyou/47585.html"
                        h="ID=SERP,5160.1"><strong>白夜琉璃</strong>手游下载-<strong>白夜琉璃</strong>手游手机安卓版v1.4.8-懒人下载</a></h2>
                <div class="b_caption">
                    <div class="b_attribution" u="1|5058|4544492236377359|iCr1uUVRGmUSmPG2Qas_VurCNnMh9v9I">
                        <cite>https://www.lanrentuku.com/shouyou/47585.html</cite><span class="c_tlbxTrg"><span class="c_tlbxH"
                                h="BASE:CACHEDPAGEDEFAULT" k="SERP,5161.1"></span></span></div>
                    <p>2021-5-11 · <strong>白夜琉璃</strong>是一款浪漫情缘<strong>题材</strong>的唯美仙侠<strong>游戏</strong>在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验，
                        。</p>
                </div>
            </li>
        """
        for curIdx, eachNormalLi in enumerate(normalLiList):
            logging.info("%s [%d] %s", "-"*10, curIdx + 1, "-"*10)

            curTitle = ""
            curUrl = ""
            curDate = ""
            curDesc = ""

            try:
                # h2AItem = eachNormalLi.find_element_by_xpath("//h2/a")
                h2AItem = eachNormalLi.find_element_by_xpath(".//h2/a")
            except:
                logging.error("Failed to find title(h2 a) element")
                continue

            curTitle = h2AItem.text
            curUrl = h2AItem.get_attribute("href")
            logging.info("curTitle=%s, curUrl=%s", curTitle, curUrl)

            try:
                descItem = eachNormalLi.find_element_by_xpath(".//div[@class='b_caption']/p")

                curDesc = descItem.text
                logging.info("curDesc=%s", curDesc) # 2021-5-11 · 白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验， 。
            except:
                logging.warning("Failed to find description(div[b_caption]/p) element")
                # continue

            if not curDesc:
                # try to find b_richcard 's tab-content
                # Note: here for b_richcard only parse first tab content as description
                """
                    <div class="b_caption">
                        <div class="b_attribution" u="8|5066|4611540973649931|HIyGQVh1PBQxFgDgJoDdz6j7pUw3Fhlb">
                            <cite>https://zhuanlan.zhihu.com/p/121145399</cite><span class="c_tlbxTrg"><span class="c_tlbxH"
                                    h="BASE:CACHEDPAGEDEFAULT" k="SERP,5255.1"></span></span></div>
                        <div class="b_richcard">
                            <div class="rc_herotabheader">
                            ...
                                    <div class="tab-content">
                                        <div id="tab_2" data-appns="SERP" data-k="5363.2" role="tabpanel" aria-labelledby="tab_2_head"
                                            data-priority="">
                                            <ul class="b_vList b_divsec">
                                                <li data-priority="">
                                                    <div><span
                                                            title="经典即时战略游戏（RTS）《帝国时代》系列，可谓是许多玩家的“童年回忆”。作者也是“帝国”的老玩家了，现在时不时还会开上一两把。 《帝国时代》（Age of Empires）是微软公司开发的即时战略游戏，游戏中玩家可以扮演不同文明在历史长河中的各个时代发展经济、建造城市，也可以通过训练军队发动战争征服其他文明。 初代游戏设定为人类史前的石器时代发展到铁器时代的过程（石器时代—工具时代—青铜时代—铁器时代），第二代游戏主要讲述中世纪历史（黑暗时代—封建时代—城堡时代—帝王时代）；第三代游戏在玩法上与前代有所不同，讲述的是地理大发现之后欧洲列强探索、殖民新大陆的故事（发现时代—殖民时代—堡垒时代—工业时代—帝国时代/革命），游戏资料片《酋长》中新增了美洲土著文明：易洛魁、苏族与阿兹特克，玩家可以选择使用原住民与欧洲列强进行对抗，资料片《亚洲王朝》则将美洲土著更换为亚洲三大文明：中华文明、日本文明和印度文明。 《帝国时代终极版》其实是《帝国时代》初代游戏的复刻版本（PC端目前仅支持在Windows10系统运行），体验远古文明从野蛮到智慧的转变。 第二代游戏可谓系列游戏中的最经典之作，游戏有丰富的剧本战役，也可以进行多样的标准游戏（我最喜欢的模式是弑君模式），还有“帝国”系列最有趣的“自建地图”地图编辑器，玩家可以通过编辑器创建自己的剧本，书写时代英雄的故事。 第三代游戏玩法上与前两代大不相同，新增“主城”概念（就是殖民国家的首都），玩家可以在标准游戏中创建主城，游戏中主城可以运送物资到殖民地，玩家也可以“装饰”主城，让其更“漂亮”。不过本作中文明数量大大减少，原版只有8个列强国家（英国、法国、普鲁士、荷兰、西班牙、葡萄牙、俄罗斯、奥斯曼）。三代的游戏画面也更进为3D画面，剧本战役也更加生动，新增的许多概念也让其与前两代游戏相比有了极大的区别度。 在《帝国时代》中担任国王、扮演将军征战沙场，指挥军队，也是一件很有趣（上瘾）的事情呢。 据说《帝国时代4》将在未来发售，还是很期待“老帝国”的新作的！">经典即时战略游戏（RTS）《帝国时代》系列，可谓是许多玩家的“童年回忆”。作者也是“帝国”的老玩家了，现在时不时还会开上一两把。
                                                            《帝国时代》（Age of
                                                            Empires）是微软公司开发的即时战略游戏，游戏中玩家可以扮演不同文明在历史长河中的各个时代发展经济、建造城市，也可以通过训练军队发动战争征服其他文明。
                                                            初代游戏设定为人类史前的石器时代发展到铁器时代的过程（石器时代—工具时代—青铜时代—铁器时代），第二代游戏主要讲述中世纪历史（黑暗时代—封建时代—城堡时代—帝王时代）；
                                                            …</span></div>
                                                </li>
                """
                try:
                    firstTabItem = eachNormalLi.find_element_by_xpath(".//div[@class='b_caption']/div[@class='b_richcard']//ul[@class='b_vList b_divsec']")
                    curDesc = firstTabItem.text
                    logging.info("curDesc=%s", curDesc) # 
                except:
                    logging.warning("Failed to find description(b_richcard first tab) element")
                    # continue

            if not curDesc:
                logging.error("Failed to find description")

            foundDate = re.search("^(?P<curDate>\d+-\d+-\d+)[\s·]*(?P<pureDesc>.+)$", curDesc)
            if foundDate:
                curDate = foundDate.group("curDate") # '2021-5-11'
                pureDesc = foundDate.group("pureDesc") # '白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验， 。'
                logging.info("curDate=%s, pureDesc=%s", curDate, pureDesc)
                curDesc = pureDesc

            curSearchResultDict = {
                "url": curUrl,
                "title": curTitle,
                "date": curDate,
                "description": curDesc,
            }
            logging.info("curSearchResultDict=%s", curSearchResultDict)
            searchResultDictList.append(curSearchResultDict)

        # first ad item
        """
            <li class="b_ad">
                <ul>
                    <li class="b_adLastChild">
                        <div class="sb_add sb_adTA">
                            <h2><a id="tile_link_cn" target="_blank" class=" b_restorableLink"
                                    onmousedown="ad_pt_mousedown_cn(this)" onmouseup="ad_pt_mouseup_cn(this)"
                                    href="http://e.so.com/search/eclk?p=dac8DLoMp5KV6LLF4qKf_LLuqlgwadNTcdmVwLMv6rJu6AEsht7C_darl2_QXquzKxu0sJtliKThz1xVpI8DRTMcm5djUgKARzVcTToe5bHpa-jCy3BuA7arrxd641N3fJB6PThDEBq0U5VGAk502OHWwE4XHTap6_FZszlE2SpV8BP8-VUJahRWYxcPOASP_O158ojqdBncS4QMzSW6F3bFmSPtjq_D-2WY1EjdTIWJktETB_Oi5GWHQKA1yJilQFMZVhQmsmshEOyTRHUkU5-YXR9dAoHhD-Y4iDUGdNKQNpa8LGBIiD97Iw75ekuWE79cYm0F4mMvB2Cg4xiNTKYAX3sVtILG3STUtVRzySKCu0xwUDbXB-_u0x2KiUzXcDZD1ymgU0p5EK2l2TSi5yamarcfRrpMF9eKP_L-S2ENmns4BP5DlEN0S_XQ_vlbG8To_6ssqiEKdJmGj0JVm8iGlut8fEfcEA8DA0ZxVw0We1_kulRatXYapd64MmShssGx__K5GNZeGpfhJaZhWzd7j26QJi5kBblTut9oIJhJ0vtOtaGvC4zKiw1MwayTxbh32OpuXhnxkghgaqKzj5hzyHsXfhVHtBp5RpIld_ZEbz5jlILD2vlSBsAiiA15GYdrStSqJfF-l4IKhNcg9sq27zlCzQGc9Sv3of_R9tE-vCtM5vYEUYUmbXxjtxCBdn0-Uy7NDTkgqfBEdBxOtvzKofGd897G02A5j2HDLgeCV37kew&amp;ns=0&amp;v=2&amp;at=AeeZveWknOeQieeSg-a4uOaIjwJfMjAyMQHnmb3lpJznkInnkoMC55S16ISR54mIX-eCueWHu-i_m-WFpQHmuLjmiI8C&amp;aurl=aHR0cDovL2x1Y2suc25nODg5LmNvbS9vbi95eC1zeS94aWFueGlhNDEvczUvY2NpZDAyNjgv&amp;sig=09e3&amp;bt=1"
                                    h="ID=SERP,5397.1,Ads"><strong>白夜琉璃游戏</strong>_2021<strong>白夜琉璃</strong>电脑版_点击进入<strong>游戏</strong></a>
                            </h2>
                            <div class="b_caption">
                                <div class="b_attribution"><cite>luck.sng889.com</cite></div>
                                <p class=""><span class="b_adProvider">来自
                                        360</span>2021免费仙侠<strong>游戏</strong>「<strong>白夜琉璃</strong>」,全新地图,爆率升级!结婚组队,自由PK!「<strong>白夜琉璃</strong>」今日新服开启,注册送首充,送VIP!<span
                                        class="b_adSlug b_opttxt b_divdef">广告</span></p>
                            </div>
                            <div class="ad_fls">
        ...
                            </div>
                        </div>
                    </li>
                </ul>
            </li>
        """

        # bottom ad item
        """
            <li class="b_ad b_adBottom">
                <ul>
                    <li class="b_adLastChild">
                        <div class="sb_add sb_adTA">
                            <h2><a id="tile_link_cn" target="_blank" class=" b_restorableLink"
                                    onmousedown="ad_pt_mousedown_cn(this)" onmouseup="ad_pt_mouseup_cn(this)"
                                    href="http://e.so.com/search/eclk?p=dac8DLoMp5KV6LLF4qKf_LLuqlgwadNTcdmVwLMv6rJu6AEsht7C_darl2_QXquzKxu0sJtliKThz1xVpI8DRTMcm5djUgKARzVcTToe5bHpa-jCy3BuA7arrxd641N3fJB6PThDEBq0U5VGAk502OHWwE4XHTap6_FZszlE2SpV8BP8-VUJahRWYxcPOASP_O158ojqdBncS4QMzSW6F3bFmSPtjq_D-2WY1EjdTIWJktETB_Oi5GWHQKA1yJilQFMZVhQmsmshEOyTRHUkU5-YXR9dAoHhD-Y4iDUGdNKQNpa8LGBIiD97Iw75ekuWE79cYm0F4mMvB2Cg4xiNTKYAX3sVtILG3STUtVRzySKCu0xwUDbXB-_u0x2KiUzXcDZD1ymgU0p5EK2l2TSi5yamarcfRrpMF9eKP_L-S2ENmns4BP5DlEN0S_XQ_vlbG8To_6ssqiEKdJmGj0JVm8iGlut8fEfcEA8DA0ZxVw0We1_kulRatXYapd64MmShssGx__K5GNZeGpfhJaZhWzd7j26QJi5kBblTut9oIJhJ0vtOtaGvC4zKiw1MwayTxbh32OpuXhnxkghgaqKzj5hzyHsXfhVHtBp5RpIld_ZEbz5jlILD2vlSBsAiiA15GYdrStSqJfF-l4IKhNcg9sq27zlCzQGc9Sv3of_R9tE-vCtM5vYEUYUmbXxjtxCBdn0-Uy7NDTkgqfBEdBxOtvzKofGd897G02A5j2HDLgeCV37kew&amp;ns=0&amp;v=2&amp;at=AeeZveWknOeQieeSg-a4uOaIjwJfMjAyMQHnmb3lpJznkInnkoMC55S16ISR54mIX-eCueWHu-i_m-WFpQHmuLjmiI8C&amp;aurl=aHR0cDovL2x1Y2suc25nODg5LmNvbS9vbi95eC1zeS94aWFueGlhNDEvczUvY2NpZDAyNjgv&amp;sig=09e3&amp;bt=1"
                                    h="ID=SERP,5412.1,Ads"><strong>白夜琉璃游戏</strong>_2021<strong>白夜琉璃</strong>电脑版_点击进入<strong>游戏</strong></a>
                            </h2>
                            <div class="b_caption">
                                <div class="b_attribution"><cite>luck.sng889.com</cite></div>
                                <p class=""><span class="b_adProvider">来自
                                        360</span>2021免费仙侠<strong>游戏</strong>「<strong>白夜琉璃</strong>」,全新地图,爆率升级!结婚组队,自由PK!「<strong>白夜琉璃</strong>」今日新服开启,注册送首充,送VIP!<span
                                        class="b_adSlug b_opttxt b_divdef">广告</span></p>
                            </div>
                        </div>
                    </li>
                </ul>
            </li>
        """
        if isIncludeAd:
            adSearchResultList = []

            adLiXpath = ".//li[starts-with(@class, 'b_ad')]"
            adLiList = resultElem.find_elements_by_xpath(adLiXpath)
            adLiNum = len(adLiList)
            logging.info("adLiNum=%s", adLiNum)

            for eachAdElem in adLiList:
                curAdTitle = ""
                curAdUrl = ""
                curAdDate = ""
                curAdDesc = ""

                try:
                    titleElem = eachAdElem.find_element_by_xpath(".//h2/a[@id='tile_link_cn']")
                    curAdTitle = titleElem.text
                    curAdUrl = titleElem.get_attribute("href")
                except:
                    logging.warning("Failed to find ad title (h2 a[tile_link_cn]) element")
                    continue

                try:
                    descElem = eachAdElem.find_element_by_xpath(".//div[@class='b_caption']//p")
                    curAdDesc = descElem.text
                except:
                    logging.warning("Failed to find ad title (div p) element")

                curAdSearchResultDict = {
                    "url": curAdUrl,
                    "title": curAdTitle,
                    "date": curAdDate,
                    "description": curAdDesc,
                }
                logging.info("curAdSearchResultDict=%s", curAdSearchResultDict)
                adSearchResultList.append(curAdSearchResultDict)

            searchResultDictList.extend(adSearchResultList)

    return searchResultDictList
```

## 输出结果

（某次）调试的输出结果：

```bash
normalLiNum=10
---------- [1] ----------
curTitle=白夜琉璃手游下载-白夜琉璃手游手机安卓版v1.4.8-懒人下载, curUrl=https://www.lanrentuku.com/shouyou/47585.html
curDesc=2021-5-11 · 白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验， 。
curDate=2021-5-11, pureDesc=白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验， 。
curSearchResultDict={'url': 'https://www.lanrentuku.com/shouyou/47585.html', 'title': '白夜琉璃手游下载-白夜琉璃手游手机安卓版v1.4.8-懒人下载', 'date': '2021-5-11', 'description': '白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，多样的挑战将给每个玩家带去无比真实的修行体验， 。'}
---------- [2] ----------
curTitle=白夜琉璃手游下载-白夜琉璃手游内测版v1.4.8-第五驱动, curUrl=http://www.drv5.cn/azgame/77154.html
curDesc=2021-5-11 · 白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界， 。
curDate=2021-5-11, pureDesc=白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界， 。
curSearchResultDict={'url': 'http://www.drv5.cn/azgame/77154.html', 'title': '白夜琉璃手游下载-白夜琉璃手游内测版v1.4.8-第五驱动', 'date': '2021-5-11', 'description': '白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界， 。'}
---------- [3] ----------
curTitle=白夜琉璃下载-白夜琉璃手游手机正式版v1.4.8, curUrl=http://www.nwmie.com.cn/azgame/66540.html
curDesc=2021-5-11 · 白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验， 。
curDate=2021-5-11, pureDesc=白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验， 。
curSearchResultDict={'url': 'http://www.nwmie.com.cn/azgame/66540.html', 'title': '白夜琉璃下载-白夜琉璃手游手机正式版v1.4.8', 'date': '2021-5-11', 'description': '白夜琉璃是一款浪漫情缘题材的唯美仙侠游戏在不断的磨砺与战斗之中强大自身，让你能够更好的融入到这个修行者的世界，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验， 。'}
---------- [4] ----------
curTitle=白夜琉璃手游下载-白夜琉璃 安卓版v1.0.1_游戏资讯网, curUrl=https://www.infogame.cn/yx/153730.html
curDesc=2021-6-18 · 白夜琉璃这是一个特别古代仙侠风格题材大型手机端网游，白夜琉璃让喜欢中国古风的手游游戏玩家们体验古代仙侠游戏的令人着迷的玩法和精致细腻的画面，白夜琉璃来游戏世界满足您的仙人梦吧。
curDate=2021-6-18, pureDesc=白夜琉璃这是一个特别古代仙侠风格题材大型手机端网游，白夜琉璃让喜欢中国古风的手游游戏玩家们体验古代仙侠游戏的令人着迷的玩法和精致细腻的画面，白夜琉璃来游戏世界满足您的仙人梦吧。
curSearchResultDict={'url': 'https://www.infogame.cn/yx/153730.html', 'title': '白夜琉璃手游下载-白夜琉璃 安卓版v1.0.1_游戏资讯网', 'date': '2021-6-18', 'description': '白夜琉璃这是一个特别古代仙侠风格题材大型手机端网游，白夜琉璃让喜欢中国古风的手游游戏玩家们体验古代仙侠游戏的令人着迷的玩法和精致细腻的画面，白夜琉璃来游戏世界满足您的仙人梦吧。'}
---------- [5] ----------
curTitle=白夜琉璃手游-白夜琉璃手游官方安卓版-雨林木风, curUrl=https://www.ylmfu.com/zhuti/45595.html
curDesc=2021-5-25 · 白夜琉璃是一款能够带给玩家超爽仙灵修道冒险的RPG手游，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界，在不断的磨砺与战斗之中强大自身。
curDate=2021-5-25, pureDesc=白夜琉璃是一款能够带给玩家超爽仙灵修道冒险的RPG手游，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界，在不断的磨砺与战斗之中强大自身。
curSearchResultDict={'url': 'https://www.ylmfu.com/zhuti/45595.html', 'title': '白夜琉璃手游-白夜琉璃手游官方安卓版-雨林木风', 'date': '2021-5-25', 'description': '白夜琉璃是一款能够带给玩家超爽仙灵修道冒险的RPG手游，在这个血色的玄幻世界里可以体验到无比精彩的战斗，多样的挑战将给每个玩家带去无比真实的修行体验，让你能够更好的融入到这个修行者的世界，在不断的磨砺与战斗之中强大自身。'}
---------- [6] ----------
curTitle=白夜琉璃游戏下载-白夜琉璃完整版免费下载v1.0-七度网, curUrl=https://m.7do.net/game/108503.html
curDesc=2021-5-11 · 白夜琉璃是一款经典趣味的仙侠手游，游戏中的玩法非常丰富十分具有趣味性，操作简单，新人上线还能获得超大礼包，帮助你一天神装，打怪更加轻松。精致的画面设计加上炫酷的特效设计，给玩家带来精致的游戏体验，玩法丰富喜欢就快来下载白夜琉璃吧！
curDate=2021-5-11, pureDesc=白夜琉璃是一款经典趣味的仙侠手游，游戏中的玩法非常丰富十分具有趣味性，操作简单，新人上线还能获得超大礼包，帮助你一天神装，打怪更加轻松。精致的画面设计加上炫酷的特效设计，给玩家带来精致的游戏体验，玩法丰富喜欢就快来下载白夜琉璃吧！
curSearchResultDict={'url': 'https://m.7do.net/game/108503.html', 'title': '白夜琉璃游戏下载-白夜琉璃完整版免费下载v1.0-七度网', 'date': '2021-5-11', 'description': '白夜琉璃是一款经典趣味的仙侠手游，游戏中的玩法非常丰富十分具有趣味性，操作简单，新人上线还能获得超大礼包，帮助你一天神装，打怪更加轻松。精致的画面设计加上炫酷的特效设计，给玩家带来精致的游戏体验，玩法丰富喜欢就快来下载白夜琉璃吧！'}
---------- [7] ----------
curTitle=白夜琉璃修真诀手游下载-白夜琉璃修真诀安卓版-旭宁下载站, curUrl=http://www.xuningbo.com/game/9508.html
curDesc=2021-7-26 · 白夜琉璃修真诀手游是一款带来有趣体验的战斗主题游戏。实时武术对战，创造精彩局面。有趣的童话来得凶猛。令人震惊的挑战解开你激动人心的童话。不同角色一起挑战。自由组队，体验新的乐趣。网上语音交流和互动都挺方便的。
curDate=2021-7-26, pureDesc=白夜琉璃修真诀手游是一款带来有趣体验的战斗主题游戏。实时武术对战，创造精彩局面。有趣的童话来得凶猛。令人震惊的挑战解开你激动人心的童话。不同角色一起挑战。自由组队，体验新的乐趣。网上语音交流和互动都挺方便的。
curSearchResultDict={'url': 'http://www.xuningbo.com/game/9508.html', 'title': '白夜琉璃修真诀手游下载-白夜琉璃修真诀安卓版-旭宁下载站', 'date': '2021-7-26', 'description': '白夜琉璃修真诀手游是一款带来有趣体验的战斗主题游戏。实时武术对战，创造精彩局面。有趣的童话来得凶猛。令人震惊的挑战解开你激动人心的童话。不同角色一起挑战。自由组队，体验新的乐趣。网上语音交流和互动都挺方便的。'}
---------- [8] ----------
curTitle=白夜琉璃剑歌起手游下载-白夜琉璃剑歌起手游官方版 v1.0 ..., curUrl=https://game.shouji.com.cn/game/186936700.html
curDesc=2021-5-12 · 游戏简介 白夜琉璃剑歌起手游是一款精彩修仙玩法的RPG战斗手游。游戏玩家你来到了这个战斗玩法丰富的仙界的当中，当下属于玩家你的战斗就从现在开始了，玩家你除了要通过战斗去提升自己的人物实力之外你后续也要完成属于你的修炼，强化自己能力同时最终成为仙界的真正强者。
curDate=2021-5-12, pureDesc=游戏简介 白夜琉璃剑歌起手游是一款精彩修仙玩法的RPG战斗手游。游戏玩家你来到了这个战斗玩法丰富的仙界的当中，当下属于玩家你的战斗就从现在开始了，玩家你除了要通过战斗去提升自己的人物实力之外你后续也要完成属于你的修炼，强化自己能力同时最终成为仙界的真正强者。
curSearchResultDict={'url': 'https://game.shouji.com.cn/game/186936700.html', 'title': '白夜琉璃剑歌起手游下载-白夜琉璃剑歌起手游官方版 v1.0 ...', 'date': '2021-5-12', 'description': '游戏简介 白夜琉璃剑歌起手游是一款精彩修仙玩法的RPG战斗手游。游戏玩家你来到了这个战斗玩法丰富的仙界的当中，当下属于玩家你的战斗就从现在开始了，玩家你除了要通过战斗去提升自己的人物实力之外你后续也要完成属于你的修炼，强化自己能力同时最终成为仙界的真正强者。'}
---------- [9] ----------
curTitle=玩家最多的仙侠手游-2021玩家最多的仙侠手游合集, curUrl=http://www.rsdown.cn/s/wjzddxxsy/
curDesc=2021-7-1 · 白夜琉璃剑歌起 游戏大小：291.36 MB 白夜琉璃剑歌起，这是款十大良心系列的仙侠手游，画面风格看起来非常舒适，久玩不腻哦，再加上人物形象颜值高，不管是妹子还是男同胞们都会爱上这款仙侠手游，感受着全新不一样修仙乐趣体验，喜欢 ...
curDate=2021-7-1, pureDesc=白夜琉璃剑歌起 游戏大小：291.36 MB 白夜琉璃剑歌起，这是款十大良心系列的仙侠手游，画面风格看起来非常舒适，久玩不腻哦，再加上人物形象颜值高，不管是妹子还是男同胞们都会爱上这款仙侠手游，感受着全新不一样修仙乐趣体验，喜欢 ...
curSearchResultDict={'url': 'http://www.rsdown.cn/s/wjzddxxsy/', 'title': '玩家最多的仙侠手游-2021玩家最多的仙侠手游合集', 'date': '2021-7-1', 'description': '白夜琉璃剑歌起 游戏大小：291.36 MB 白夜琉璃剑歌起，这是款十大良心系列的仙侠手游，画面风格看起来非常舒适，久玩不腻哦，再加上人物形象颜值高，不管是妹子还是男同胞们都会爱上这款仙侠手游，感受着全新不一样修仙乐趣体验，喜欢 ...'}
---------- [10] ----------
curTitle=【历史】游戏与历史：历史题材游戏分享（上） - 知乎, curUrl=https://zhuanlan.zhihu.com/p/121145399
curDesc=当今游戏产业电竞产业可谓快速发展，当然作者和电竞大佬们是比不了了，不过作者也有钟爱的游戏——历史题材游戏，今天就来和大家分享一下下~ （适当游戏娱乐健康，过度游戏伤身败业） 一、《帝国 …
curSearchResultDict={'url': 'https://zhuanlan.zhihu.com/p/121145399', 'title': '【历史】游戏与历史：历史题材游戏分享（上） - 知乎', 'date': '', 'description': '当今游戏产业电竞产业可谓快速发展，当然作者和电竞大佬们是比不了了，不过作者也有钟爱的游戏——历史题材游戏，今天就来和大家分享一下下~ （适当游戏娱乐健康，过度游戏伤身败业） 一、《帝国 …'}
```
