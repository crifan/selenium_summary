# selenium-wire

* `selenium-wire`
  * 是什么：Selenium的一个插件
  * 功能：可以捕获和访问到底层的浏览器发出的请求和响应
  * 主页
    * GitHub
      * https://github.com/wkeeling/selenium-wire

## 官网示例

```python
from seleniumwire import webdriver  # Import from seleniumwire

# Create a new instance of the Chrome driver
driver = webdriver.Chrome()

# Go to the Google home page
driver.get('https://www.google.com')

# Access requests via the `requests` attribute
for request in driver.requests:
    if request.response:
        print(
            request.url,
            request.response.status_code,
            request.response.headers['Content-Type']
        )
```

输出：

```bash
https://www.google.com/ 200 text/html; charset=UTF-8
https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_120x44dp.png 200 image/png
https://consent.google.com/status?continue=https://www.google.com&pc=s&timestamp=1531511954&gl=GB 204 text/html; charset=utf-8
https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png 200 image/png
https://ssl.gstatic.com/gb/images/i2_2ec824b0.png 200 image/png
https://www.google.com/gen_204?s=webaft&t=aft&atyp=csi&ei=kgRJW7DBONKTlwTK77wQ&rt=wsrt.366,aft.58,prt.58 204 text/html; charset=UTF-8
...
```

## 基本用法

* 安装

```bash
pipenv install selenium-wire
```

* 更新代码

把之前的：

```python
from selenium import webdriver
```

改为：

```python
from seleniumwire import webdriver
```

其他（一般的Selenium的）代码，基本不用变。

* 具体使用：捕获http请求

在用：

```python
driver.get(inputUrl)
```

加载页面后，用：

```python
  # capture http request and response
  # Access requests via the `requests` attribute
  requestNum = len(driver.requests)
  logging.info("Captured %d requests", requestNum)
  for curIdx, curReq in enumerate(driver.requests):
      curNum = curIdx + 1
      curUrl = curReq.url
      if curReq.response:
          curResp = curReq.response
          logging.info("[%d] resp: url:%s, code=%s, Content-Type=%s", 
              curNum, curUrl, curResp.status_code, curResp.headers['Content-Type'])
```

即可获取到每一个request（和对应response）。

之后，即可根据自己业务逻辑，去利用（每一个）request（和response）了。

* 说明
  * 初始化期间会打印出log
    ```bash
    backend.py:51   INFO    Created proxy listening on ::ffff:127.0.0.1:64784
    ```
  * 而`driver.get`后，会输出相关捕获到的请求和响应
    ```bash
    20210722 03:33:05 handler.py:57   INFO    Capturing request: https://urldx.cn/9MUPowKt?sVmW
    20210722 03:33:05 handler.py:116  INFO    Capturing response: https://urldx.cn/9MUPowKt?sVmW 302 Found
    ...
    20210722 03:33:05 handler.py:57   INFO    Capturing request: https://s.k4l.cn/games/all_css/common_v20210407.css
    ...
    ```

## 其他

### 禁止捕获请求

可以额外增加参数，（临时）禁止捕获http请求：

```python
options = {
    'disable_capture': True  # Don't intercept/store any requests.
}
driver = webdriver.Chrome(seleniumwire_options=options)
```
