# Python爬虫

# Robots协议

Robots Exclusion Standard网络爬虫排除标准
作用:网站告知网络爬虫哪些页面可以抓取，哪些不行。
形式:在网站根目录下的robots.txt文件。

查看方法：在网址后面加/robots.txt

# 爬虫库

## ruquests

### requests的安装

启动cmd命令   pip install requests

![image-20200325165116603](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325165116603.png)

ep:

```python
import requests
>>> r = requests.get("http://www.baidu.com")
>>> r.status_code
200
>>> r.encoding = 'utf-8'
>>> r.text
>>> type(r)
<class 'requests.models.Response'>
>>>r.headers
{'Cache-Control': 'private, no-cache, no-store, proxy-revalidate, no-transform', 'Connection': 'keep-alive', 'Content-Encoding': 'gzip', 'Content-Type': 'text/html', 'Date': 'Wed, 25 Mar 2020 08:58:42 GMT', 'Last-Modified': 'Mon, 23 Jan 2017 13:27:32 GMT', 'Pragma': 'no-cache', 'Server': 'bfe/1.0.8.18', 'Set-Cookie': 'BDORZ=27315; max-age=86400; domain=.baidu.com; path=/', 'Transfer-Encoding': 'chunked'}
```

#### 问题：SyntaxError: multiple statements found while compiling a single statement

```python
import requests
>>> r = requests.get("http://www.baidu.com")
>>> r.status_code
SyntaxError: multiple statements found while compiling a single statement
```

解决方法：

方法一：先将第一行复制，敲一下回车，再将剩下的部分复制过去，运行；

方法二：Ctrl+N，新建一个，这时直接将代码复制进来，就不会产生这个问题了；直接在IDLE中编译，是每行都要回车的。如果是单独的语句，只能是一行一行的编辑。、

![img](https://iknow-pic.cdn.bcebos.com/a8773912b31bb0517db0fcd53d7adab44bede0b3?x-bce-process=image/resize,m_lfit,w_600,h_800,limit_1)

![image-20200325170150679](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325170150679.png)

##### requests.get()

```python
r = requests.get(url)
```

r ：Response  访问返回的数据

 ![image-20200325172312082](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325172312082.png)

Response 对象属性

![image-20200325180203743](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325180203743.png)

![image-20200325183329707](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325183329707.png)

```python
>>> kv={'key1':'value1','key2':'value2'}
>>> r = requests.request('GET','http://python123.io/ws',params=kv)
>>> print(r.url)
https://python123.io/ws?key1=value1&key2=value2
```

## BeautifulSoup

### BeautifulSoup的安装

打开cmd 输入 pip install beautifulsoup4

![image-20200325211038450](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325211038450.png)

### BeautifulSoup 的使用

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup('<p>data</p>','html.parser')
```

或者

```python
import bs4
soup = BeautifulSoup('<p>data</p>','html.parser')
```

ep:

```python
>>> import requests
>>> r = requests.get('https://python123.io/ws/demo.html')
>>> r.text
>>> demo = r.text
>>> from bs4 import BeautifulSoup
>>> soup = BeautifulSoup(demo,'html.parser')
>>> print(soup.prettify())
```

![image-20200325212111010](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325212111010.png)

### BeautifulSoup库的元素

### 基于bs4的HTML内容查找方法

```python
.find_all(name,attrs,recursive,string,**kwargs)
#返回一个列表类型，存储查找的结果
```

name:对标签名称的检索字符串

```python
soup.find_all('a')
#查找所有a标签
soup.find_all(['a','b'])
#查找所有a标签和b标签
```

参数给True，则显示所有标签

```python
for tag in soup.find_all(True):
  print(tag.name)
```

只打印以b开头的标签，引用正则表达式库

```python
import re
for tag in soup.find_all(re.compile('b')):
  print(tag.name)
```

attrs:对标签属性值的检索字符串，可标注属性检索

```python
soup.find_all('p','course')
#查找属性值为course的p标签信息

soup.find_all(di = 'link1')
#查找id值为link1的标签信息

import re
soup.find_all(id = re.compile('link'))
#查找所有以link开头的id值的标签信息
```

recursive：是对子孙全部检索，默认True

string:<>...</>中字符串区域的检索字符串

```python
soup.find_all(string = 'Basci Python')
#只查找Basic Python

import re
soup.find_all(string = re.compile('python'))
#查找所有带python字样的字符串信息
```

![image-20200326110721947](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200326110721947.png)

![image-20200326110842090](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200326110842090.png)

![image-20200326110901824](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200326110901824.png)

# 爬虫框架

## scrapy

![image-20200329123441710](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329123441710.png)

![image-20200329124915218](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329124915218.png)

![image-20200329130212674](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329130212674.png)

![image-20200329130738654](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329130738654.png)

![image-20200329131244391](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329131244391.png)



![image-20200329132023557](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329132023557.png)







![image-20200329132406279](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329132406279.png)

![image-20200329132429543](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329132429543.png)





# 正则表达式

![image-20200326123949778](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200326123949778.png)

## Re库的使用

```python
import re
r'[1-9]\d{5}'
```



![image-20200326124331335](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200326124331335.png)

![image-20200329111528130](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329111528130.png)

![image-20200329111909557](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329111909557.png)

![image-20200329111933681](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329111933681.png)

![image-20200329113256084](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329113256084.png)

![image-20200329113313474](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329113313474.png)

![image-20200329113345720](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200329113345720.png)











# 实战

## 1.京东商品爬取

https://item.jd.com/2967929.html

```python
>>> import requests
>>> r = requests.get("https://item.jd.com/2967929.html")
>>> r.status_code
200
>>> r.encoding
'gbk'
>>> r.text[:1000]
```

![image-20200325190404852](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325190404852.png)

## 2.亚马逊商品页面爬取

https://www.amazon.cn/gp/product/B01M8L5Z3Y

```python
>>> import requests
>>> r = requests.get("https://www.amazon.cn/gp/product/B01M8L5Z3Y")
>>> r.status_code
503
>>> r.encoding
'ISO-8859-1'
>>> r.encoding = r.apparent_encoding
>>> r.text
```

访问出错，查看header信息发现，user-agent是python

```python
>>> r.request.headers
{'User-Agent': 'python-requests/2.23.0', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive'}
```

重新设置user-agent 为Mozilla/5.0 访问成功

```python
>>> kv = {'user-agent':'Mozilla/5.0'}
>>> url="https://www.amazon.cn/gp/product/B01M8L5Z3Y"
>>> r = requests.get(url,headers=kv)
>>> r.status_code
200
>>> r.request.headers
{'user-agent': 'Mozilla/5.0', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive'}
>>> r.text
```

![image-20200325191425921](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325191425921.png)

## 3.百度360搜索关键词提交

百度关键词接口

http://www.baidu.com/s?wd=keyword

```python
>>> import requests
>>> kv = {'wd':'python'}
>>> r = requests.get("http://www.baidu.com/s",params = kv)
>>> r.status_code
200
>>> r.request.url
'https://wappass.baidu.com/static/captcha/tuxing.html?&ak=c27bbc89afca0463650ac9bde68ebe06&backurl=https%3A%2F%2Fwww.baidu.com%2Fs%3Fwd%3Dpython&logid=7327037615380438246&signature=18d2fbb016b18e6080d2bac079d397e7&timestamp=1585135084'
>>> len(r.text)
1519
```

![image-20200325192003840](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325192003840.png)

360关键词借口

http://www.so.com/s?q=keyword



![image-20200325192027331](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325192027331.png)

## 4.网络图片爬取储存

[图片链接](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585145898833&di=fe5e76e70bf380b4d6a8efb6dc6441f5&imgtype=0&src=http%3A%2F%2Fattach.bbs.miui.com%2Fforum%2F201407%2F12%2F191515sskuppax42aarano.jpg)

```python
>>> import requests
>>> path = "C:/Users/SpiderMonkey/Desktop/新建文件夹/bo.jpg"
>>> url = "https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1585145898833&di=fe5e76e70bf380b4d6a8efb6dc6441f5&imgtype=0&src=http%3A%2F%2Fattach.bbs.miui.com%2Fforum%2F201407%2F12%2F191515sskuppax42aarano.jpg"
>>> r = requests.get(url)
>>> r.status_code
200
>>> with open(path,'wb') as f:
	f.write(r.content)

	
76525
>>> f.close()
```

![image-20200325203457319](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325203457319.png)

## 5.IP归属地的查询

![image-20200325210633542](C:\Users\SpiderMonkey\AppData\Roaming\Typora\typora-user-images\image-20200325210633542.png)

## 6.中国大学排名定向爬虫

[最好大学网链接](http://www.zuihaodaxue.cn/zuihaodaxuepaiming2019.html)

## 7.steam模拟登陆

[steam链接](https://store.steampowered.com/login/?redir=&uredirssl=1)

## 8.淘宝比价定向爬虫

## 9.股票数据定向爬虫

百度股票:https://gupiao.baidu.com/stock/

新浪股票: http://finance.sina.com.cn/stock/

东方财富网: http://quote.eastmoney.com/stocklist.html

