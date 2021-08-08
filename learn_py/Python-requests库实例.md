# Python-requests库5个实例

## 实例1：京东商品页面的爬取

- https://item.jd.com/2967929.html

- IDLE:

  ```python
  >>> import requests
  >>> r = requests.get("https://item.jd.com/2967929.html")
  >>> r.status_code
  200
  >>> r.encoding
  'gbk'
  >>> r.text[:1000]
  '<!DOCTYPE HTML>\n<html lang="zh-CN">\n<head>\n    <!-- shouji -->\n    <meta http-equiv="Content-Type" content="text/html; charset=gbk" />\n    <title>【华为荣耀8】荣耀8 4GB+64GB 全网通4G手机 魅海蓝【行情 报价 价格 评测】-京东</title>\n    <meta name="keywords" content="HUAWEI荣耀8,华为荣耀8,华为荣耀8报价,HUAWEI荣耀8报价"/>\n    <meta name="description" content="【华为荣耀8】京东JD.COM提供华为荣耀8正品行货，并包括HUAWEI荣耀8网购指南，以及华为荣耀8图片、荣耀8参数、荣耀8评论、荣耀8心得、荣耀8技巧等信息，网购华为荣耀8上京东,放心又轻松" />\n    <meta name="format-detection" content="telephone=no">\n    <meta http-equiv="mobile-agent" content="format=xhtml; url=//item.m.jd.com/product/2967929.html">\n    <meta http-equiv="mobile-agent" content="format=html5; url=//item.m.jd.com/product/2967929.html">\n    <meta http-equiv="X-UA-Compatible" content="IE=Edge">\n    <link rel="canonical" href="//item.jd.com/2967929.html"/>\n        <link rel="dns-prefetch" href="//misc.360buyimg.com"/>\n    <link rel="dns-prefetch" href="//static.360buyimg.com"/>\n    <link rel="dns-prefetch" href="//img10.360buyimg.com"/>\n    <link rel="dns'
  ```

- 全代码:

  ```python
  import requests
  url = "https://item.jd.com/2967929.html"
  try:
      r = requests.get(url)
      r.raise_for_status()
      r.encoding = r.apparent_encoding
      print(r.text[:1000])
  except:
      print("爬取失败")
  ```

  

## 实例2：亚马逊商品页面的爬取

- https://www.amazon.cn/gp/product/B01M8L5Z3Y

- IDLE:

  ```python
  >>> import requests
  >>> r = requests.get("https://www.amazon.cn/gp/product/B01M8L5Z3Y")
  >>> r.status_code
  503
  >>> r.encoding
  'ISO-8859-1'
  >>> r.encoding = r.apparent_encoding
  >>> r.text[2000:4000]
  '     <i class="a-icon a-icon-alert"></i>\n                <h4>请输入您在下方看到的字符</h4>\n                <p class="a-last">抱歉，我们只是想确认一下当前访问者并非自动程序。为了达到最佳效果，请确保您浏览器上的 Cookie 已启用。</p>\n                </div>\n            </div>\n\n            <div class="a-section">\n\n                <div class="a-box a-color-offset-background">\n                    <div class="a-box-inner a-padding-extra-large">\n\n                        <form method="get" action="/errors/validateCaptcha" name="">\n                            <input type=hidden name="amzn" value="NXqI635zDoDHEcNtYuDg/A==" /><input type=hidden name="amzn-r" value="&#047;gp&#047;product&#047;B01M8L5Z3Y" />\n                            <div class="a-row a-spacing-large">\n                                <div class="a-box">\n                                    <div class="a-box-inner">\n                                        <h4>请输入您在这个图片中看到的字符：</h4>\n                                        <div class="a-row a-text-center">\n                                            <img src="https://images-na.ssl-images-amazon.com/captcha/kwizfixk/Captcha_rowfabxzxk.jpg">\n                                        </div>\n                                        <div class="a-row a-spacing-base">\n                                            <div class="a-row">\n                                                <div class="a-column a-span6">\n                                                    <label for="captchacharacters">输入字符</label>\n                                                </div>\n                                                <div class="a-column a-span6 a-span-last a-text-right">\n                                                    <a onclick="window.location.reload()">换一张图</a>\n                                                </div>\n                                            </div>\n                                            <input autocomplete="off" spellcheck="false" id="captchacharacters" name="field-keywords" class="a-span12" autocapitalize="off" autoc'
  >>> r.request.headers
  {'User-Agent': 'python-requests/2.23.0', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive'}
  >>> kv = {'User-Agent':'Mozilla/5.0'}
  >>> url = "https://www.amazon.cn/gp/product/B01M8L5Z3Y"
  >>> r = requests.get(url,headers = kv)
  >>> r.status_code
  200
  >>> r.request.headers
  {'User-Agent': 'Mozilla/5.0', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive'}
  >>> r.encoding = r.apparent_encoding
  >>> r.text[5000:8000]
  'mall a-size-mini">\n            <a href="https://www.amazon.cn/gp/help/customer/display.html/ref=footer_claim?ie=UTF8&nodeId=200347160">使用条件</a>\n            <span class="a-letter-space"></span>\n            <span class="a-letter-space"></span>\n            <span class="a-letter-space"></span>\n            <span class="a-letter-space"></span>\n            <a href="https://www.amazon.cn/gp/help/customer/display.html/ref=footer_privacy?ie=UTF8&nodeId=200347130">隐私声明</a>\n        </div>\n\n        <div class="a-text-center a-size-mini a-color-secondary">\n          &copy; 1996-2015, Amazon.com, Inc. or its affiliates\n          <script>\n           if (true === true) {\n             document.write(\'<img src="https://fls-cn.amaz\'+\'on.cn/\'+\'1/oc-csi/1/OP/requestId=K1C54EGF6KEV9G4R3MCY&js=1" />\');\n           };\n          </script>\n          <noscript>\n            <img src="https://fls-cn.amazon.cn/1/oc-csi/1/OP/requestId=K1C54EGF6KEV9G4R3MCY&js=0" />\n          </noscript>\n        </div>\n    </div>\n    <script>\n    if (true === true) {\n        var elem = document.createElement("script");\n        elem.src = "https://images-cn.ssl-images-amazon.com/images/G/01/csminstrumentation/csm-captcha-instrumentation.min._V" + (+ new Date()) + "_.js";\n        document.getElementsByTagName(\'head\')[0].appendChild(elem);\n    }\n    </script>\n</body></html>\n'
  ```

- 全代码

  ```python
  import requests
  url = "https://www.amazon.cn/gp/product/B01M8L5Z3Y"
  try:
      kv = {'User-Agent':'Mozilla/5.0'}
      r= requests.get(url,headers=kv)
      r.raise_for_status()
      r.encoding = r.apparent_encoding
      print(r.text[5000:8000])
  except:
      print("爬取失败")
  ```

  

## 实例3：百度/360搜索关键字提交

- 百度:http://www.baidu.com

  - 关键词提交接口:http://www.baidu.com/s?wd=keyword

  - IDLE:

    ```python
    >>> import requests
    >>> url = "https://baidu.com/s"
    >>> kv = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134"}
    >>> r = requests.get(url,params={'wd':'python'},headers=kv)
    >>> r.request.url
    'https://www.baidu.com/s?wd=python'
    >>> len(r.text)
    442673
    ```
    
  - 全代码:

    ```python
    import requests
    keyword = "python"
    try:
        kv = {'wd':keyword}
        header = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134"}
        r = requests.get("https://www.baidu.com/s",params=kv,headers=header)
        print(r.request.url)
        r.raise_for_status()
        print(len(r.text))
    except:
        print("爬取失败")
    ```

    **算了我太菜了，百度总是出现“百度安全验证”，我搞不定，以后再说吧**

- 360:http://www.so.com

  - 关键词提交接口:http://www.so.com/s?q=keyword
  
  - IDLE:
  
    ```python
    >>> import requests
    >>> kv = {'q':'python'}
    >>> r = requests.get("https://www.so.com/s",params=kv)
    >>> r.status_code
    200
    >>> r.request.url
    'https://www.so.com/s?q=python'
    >>> len(r.text)
    306321
    ```
  
  - 全代码:
  
    ```python
    import requests
    keyword = "python"
    try:
        kv = {'q':keyword}
        r = requests.get("https://www.so.com/s",params=kv)
        print(r.request.url)
        r.raise_for_status()
        print(len(r.text))
    except:
        print("爬取失败")
    ```
  
    

## 实例4：网络图片的爬取和存储

- 图片地址:http://image.ngchina.com.cn/userpic/108164/2020/02201212391081641822.jpeg

- IDLE:

  ```python
  >>> import requests
  >>> path = "F://photo//national_geographic//test.jpg"
  >>> url = "http://image.ngchina.com.cn/userpic/108164/2020/02201212391081641822.jpeg"
  >>> r = requests.get(url)
  >>> r.status_code
  200
  >>> with open(path,'wb') as f:
  	f.write(r.content)
  984200
  >>> f.close()
  ```

- 全代码:

  ```python
  import requests
  import os
  url = "http://image.ngchina.com.cn/userpic/99679/2019/0615110031996794986.jpeg"
  root = "F://photo//scenery//"
  path = root + url.split('/')[-1]
  try:
      if not os.path.exists(root):
          os.mkdir(root)
      if not os.path.exists(path):
          r = requests.get(url)
          with open(path,'wb') as f:
              f.write(r.content)
              f.close()
              print("文件保存成功")
      else:
          print("文件已存在")
  except:
      print("爬取失败")
  ```

  

## 实例5：IP地址归属地的自动查询

- http://m.ip138.com/ip.asp?ip=ipaddress

- IDLE:

  ```python
  >>> import requests
  >>> header = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134"}
  >>> url = "http://m.ip138.com/ip.asp?ip="
  >>> r = requests.get(url+'202.204.80.112',headers=header)
  >>> r.status_code
  200
  >>> r.text[-500:]
  'alue="查询" class="form-btn" />\r\n\t\t\t\t\t</form>\r\n\t\t\t\t</div>\r\n\t\t\t\t<div class="query-hd">ip138.com IP查询(搜索IP地址的地理位置)</div>\r\n\t\t\t\t<h1 class="query">您查询的IP：202.204.80.112</h1><p class="result">本站主数据：北京市海淀区 北京理工大学 教育网</p><p class="result">参考数据一：北京理工大学 网络中心</p>\r\n\r\n\t\t\t</div>\r\n\t\t</div>\r\n\r\n\t\t<div class="footer">\r\n\t\t\t<a href="http://www.miitbeian.gov.cn/" rel="nofollow" target="_blank">沪ICP备10013467号-1</a>\r\n\t\t</div>\r\n\t</div>\r\n\r\n\t<script type="text/javascript" src="/script/common.js"></script></body>\r\n</html>\r\n'
  ```

- 全代码:

  ```python
  import requests
  header = {"User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/64.0.3282.140 Safari/537.36 Edge/17.17134"}
  url = "http://m.ip138.com/ip.asp?ip="
  try:
      r = requests.get(url+"202.204.80.112",headers=header)
      r.raise_for_status()
      r.encoding = r.apparent_encoding
      print(r.text[-500:])
  except:
      print("爬取失败")
  ```

  

