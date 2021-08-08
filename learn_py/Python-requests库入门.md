# Python-requests库入门

## HTTP协议

**HTTP，Hypertext Transfer Protocol，超文本传输协议**

- HTTP是一个基于“请求与响应”模式的、无状态的应用层协议

- HTTP协议采用URL作为定位网络资源的标识，URL格式如下：

  `http://host[:port][path]`
  
  - host: 合法的Internet主机域名或IP地址
  - port: 端口号，缺省端口为80
  - path: 请求资源的路径
  
- 方法

  |  方法  | 说明                                                         |
  | :----: | ------------------------------------------------------------ |
  |  GET   | 请求获取URL位置的资源                                        |
  |  HEAD  | HEAD 请求获取URL位置资源的响应消息报告，即获得该资源的头部信息 |
  |  POST  | POST 请求向URL位置的资源后附加新的数据                       |
  |  PUT   | PUT 请求向URL位置存储一个资源，覆盖原URL位置的资源           |
  | PATCH  | PATCH 请求局部更新URL位置的资源，即改变该处资源的部分内容    |
  | DELETE | DELETE 请求删除URL位置存储的资源                             |

   <div class="mermaid">
       graph LR
  </div>

```mermaid
graph LR
PC --URL-->cloud
PC --"PUT POST PATCH DELETE"-->cloud
cloud --"GET HEAD"-->PC
```

### *PATCH和PUT的区别*
假设URL位置有一组数据UserInfo，包括UserID、UserName等20个字段
需求：用户修改了UserName，其他不变
- 采用PATCH，仅向URL提交UserName的局部更新请求
- 采用PUT，必须将所有20个字段一并提交到URL，未提交字段被删除

PATCH的最主要好处：节省网络带宽

## requests库的2个重要对象

`r = requests.get(url)`

- **`r`为Response对象:包含爬虫返回的内容**
- request对象:请求数据的载体
### response对象的属性

|         属性          | 说明                                             |
| :-------------------: | ------------------------------------------------ |
|    `r.status_code`    | HTTP请求的返回状态，200表示连接成功，404表示失败 |
|       `r.text`        | HTTP响应内容的字符串形式，即，url对应的页面内容  |
|     `r.encoding`      | 从HTTP header中猜测的响应内容编码方式            |
| `r.apparent_encoding` | 从内容中分析出的响应内容编码方式（备选编码方式） |
|      `r.content`      | HTTP响应内容的二进制形式                         |



## requests库7个主要方法

|         方法         | 说明                                                         |
| :------------------: | ------------------------------------------------------------ |
| `requests.request()` | 构造一个请求，支撑以下各方法的基础方法                       |
|   `requests.get()`   | 获取HTML网页的主要方法，对应于HTTP的GET                      |
|  `requests.head()`   | 获取HTML网页头信息的方法，对应于HTTP的HEAD                   |
|  `requests.post()`   | 向HTML网页提交POST请求的方法，对应于HTTP的POST               |
|   `requests.put()`   | 向HTML网页提交PUT请求的方法，对应于HTTP的PUT                 |
|  `requests.patch()`  | 向HTML网页提交局部修改请求，对应于HTTP的PATCH                |
| `requests.delete()`  | requests.delete() 向HTML页面提交删除请求，对应于HTTP的DELETE |

- `requests.request(method, url, **kwargs)`

  - method : 请求方式，对应get/put/post等7种

    ```python
    r = requests.request('GET', url, **kwargs)
    r = requests.request('HEAD', url, **kwargs)
    r = requests.request('POST', url, **kwargs)
    r = requests.request('PUT', url, **kwargs)
    r = requests.request('PATCH', url, **kwargs)
    r = requests.request('delete', url, **kwargs)
    r = requests.request('OPTIONS', url, **kwargs)
    ```

  - url : 拟获取页面的url链接

  - **kwargs: 控制访问的参数，共13个
  
    - params : 字典或字节序列，作为参数增加到url中
  
      ```python
      >>> kv = {'key1': 'value1', 'key2': 'value2'}
      >>> r = requests.request('GET', 'http://python123.io/ws', params=kv)
      >>> print(r.url)
      http://python123.io/ws?key1=value1&key2=value2
      ```
      
    - data : 字典、字节序列或文件对象，作为Request的内容
    
      ```python
      >>> kv = {'key1': 'value1', 'key2': 'value2'}
      >>> r = requests.request('POST', 'http://python123.io/ws', data=kv)
      >>> body = '主体内容'
      >>> r = requests.request('POST', 'http://python123.io/ws', data=body)
      ```
      
    - json : JSON格式的数据，作为Request的内容
      
      ```python
      >>> kv = {'key1': 'value1'}
      >>> r = requests.request('POST', 'http://python123.io/ws', json=kv)
      ```
      
    - headers : 字典，HTTP定制头
    
      ```python
      >>> hd = {'user‐agent': 'Chrome/10'}
      >>> r = requests.request('POST', 'http://python123.io/ws', headers=hd)
      ```
    
    - cookies : 字典或CookieJar，Request中的cookie
    
    - auth : 元组，支持HTTP认证功能
    
    - files : 字典类型，传输文件
    
      ```python
      >>> fs = {'file': open('data.xls', 'rb')}
      >>> r = requests.request('POST', 'http://python123.io/ws', files=fs)
      ```
    
    - timeout : 设定超时时间，秒为单位
    
      ```python
      >>> r = requests.request('GET', 'http://www.baidu.com', timeout=10)
      ```
    
    - proxies : 字典类型，设定访问代理服务器，可以增加登录认证
    
      ```python
      >>> pxs = { 'http': 'http://user:pass@10.10.10.1:1234','https': 'https://10.10.10.1:4321' }
      >>> r = requests.request('GET', 'http://www.baidu.com', proxies=pxs)
      ```
    
    - allow_redirects : True/False，默认为True，重定向开关
    
    - stream : True/False，默认为True，获取内容立即下载开关
    
    - verify : True/False，默认为True，认证SSL证书开关
    
    - cert : 本地SSL证书路径
  
- `requests.get(url, params=None, **kwargs)`

  - url : 拟获取页面的url链接
  
  - params : url中的额外参数，字典或字节流格式，可选
  
  - **kwargs: 12个控制访问的参数
  
- `requests.head(url, **kwargs)`

  - url : 拟获取页面的url链接

  -  **kwargs: 12个控制访问的参数

- `requests.post(url, data=None, json=None, **kwargs)`

  - url : 拟更新页面的url链接
  - data : 字典、字节序列或文件，Request的内容
  - json : JSON格式的数据，Request的内容
  - **kwargs: 12个控制访问的参数

- `requests.put(url, data=None, **kwargs)`

  - url : 拟更新页面的url链接
  - data : 字典、字节序列或文件，Request的内容
  - **kwargs: 12个控制访问的参数

- `requests.patch(url, data=None, **kwargs)`

  - url : 拟更新页面的url链接
  - data : 字典、字节序列或文件，Request的内容
  - **kwargs: 12个控制访问的参数

- `requests.delete(url, **kwargs)`

  - url : 拟删除页面的url链接
  - **kwargs: 12个控制访问的参数

## 通用代码框架

### requests库的异常

- ` r.raise_for_status()`:如果不是200，则产生异常requests.HTTPError

  *在方法内部判断r.status_code是否等于200，不需要增加额外的if语句，该语句便于利用try‐except进行异常处理*

|            异常             | 说明                                        |
| :-------------------------: | ------------------------------------------- |
| `requests.ConnectionError`  | 网络连接错误异常，如DNS查询失败、拒绝连接等 |
|    `requests.HTTPError`     | HTTP错误异常                                |
|   `requests.URLRequired`    | URL缺失异常                                 |
| `requests.TooManyRedirects` | 超过最大重定向次数，产生重定向异常          |
|  `requests.ConnectTimeout`  | 连接远程服务器超时异常                      |
|     `requests.Timeout`      | 请求URL超时，产生超时异常                   |

### 爬取网页的通用代码框架

```python
import requests

def getHTMLText(url):
    try:
        r = requests.get(url,timeout=30)
        r.raise_for_status()#若状态不是200，引发HTTPError异常
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "产生异常"

if _name_ == "_main_":
    url = "http://www.baidu.com"
    print(getHTMLText(url))
```

