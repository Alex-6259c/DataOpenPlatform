# 1. 发送get请求

``` python
import requests
url = 'http://www.baidu.com'
response = requests.get(url)
#  
print(response.text)	# str类型 解码类型：推测的

print(response.content)	# bytes类型 解码类型：没有指定
```

# 2. response响应对象

``` python
# 手动设定编码格式
response.encoding = 'utf8'
print(response.text)
# 打印编码格式
print(response.encoding)
```

``` python
# response.content是存储的bytes类型的响应源码，可以进行decode操作
print(response.content.decode())		# 默认utf8
response.content.decode('GBK')
```

![image-20240702205848355](https://image1-1324746932.cos.ap-beijing.myqcloud.com/undefinedimage-20240702205848355.png)

# 2.1 response响应对象的其他常用属性或方法

``` python
response.url	# 实际的响应url ，可能与请求的url不一致
response.status_code	# 状态码
response.request.headers	# 响应对象对应的请求头
response.headers			# 响应头
response.request._cookies
response.cookies
response.json() #自动将json字符串类型的响应内容转换为python对象(dict or list)
```



# 3. 发送带header的请求

``` python
# 构建请求头字典
header = {
    # 字典
}
request.get(url, header = header)
```



