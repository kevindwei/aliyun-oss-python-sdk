# Aliyun OSS SDK for Python

## 概述
阿里云对象存储Python SDK 2.x版本。该版本不和上一个版本（0.x版本）兼容，包的名称为oss2，以避免和先前的版本冲突。
该版本的SDK依赖于优秀的第三方HTTP库[requests](https://github.com/kennethreitz/requests)，请按照下述安装方法进行安装。

## 运行环境
Python 2.6，2.7，3.3，3.4，3.5

**注意**：请不要使用Python 3.3.0、3.3.1，参考[Python Issue 16658](https://bugs.python.org/issue16658)

## 安装方法
通过pip安装官方发布的版本（以Linux系统为例）：
```bash
$ pip install oss2
```
也可以直接安装解压后的安装包：
```bash
$ sudo python setup.py install
```

## 快速使用
```python
# -*- coding: utf-8 -*-

import oss2

endpoint = 'http://oss-cn-hangzhou.aliyuncs.com' # 假设你的Bucket处于杭州区域

auth = oss2.Auth('<你的AccessKeyId>', '<你的AccessKeySecret>')
bucket = oss2.Bucket(auth, endpoint, '<你的Bucket名>')

# Bucket中的文件名（key）为storage.txt
key = 'story.txt'

# 上传
bucket.put_object(key, 'Ali Baba is a happy youth.')

# 下载
bucket.get_object(key).read()

# 删除
bucket.delete_object(key)

# 遍历Bucket里所有文件
for object_info in oss2.ObjectIterator(bucket):
    print(object_info.key)
```

## 出错处理
除非特别说明，一旦出错，Python SDK的接口就会抛出异常（见oss2.exceptions子模块）。参考下面的例子：
```python

try:
    result = bucket.get_object(key)
    print(result.read())
except oss2.exceptions.NoSuchKey as e:
    print('{0} not found: http_status={1}, request_id={2}'.format(key, e.result.status, e.result.request_id))
```

## 测试
首先通过环境变量来设置测试所需的AccessKeyID、AccessKeySecret、Endpoint以及Bucket信息（以Linux系统为例）：
```bash
$ export OSS_TEST_ACCESS_KEY_ID=<AccessKeyID>
$ export OSS_TEST_ACCESS_KEY_SECRET=<AccessKeySecret>
$ export OSS_TEST_ENDPOINT=<endpoint>
$ export OSS_TEST_BUCKET=<bucket>
```
然后可以通过以下方式之一运行测试：
```bash
$ python -m unittest discover tests  # 如果Python版本 >= 2.7
$ nosetests                         # 如果安装了nose
$ py.test                           # 如果安装了py.test
```
## 更多使用
- [更多例子](https://github.com/aliyun/aliyun-oss-python-sdk/tree/master/examples)
- [官网Python SDK文档](https://docs.aliyun.com/#/pub/oss/sdk/python-sdk&preface)

## 联系我们
- [阿里云OSS官方网站](http://oss.aliyun.com)
- [阿里云OSS官方论坛](http://bbs.aliyun.com)
- [阿里云OSS官方文档中心](http://www.aliyun.com/product/oss#Docs)
- 阿里云官方技术支持：[提交工单](https://workorder.console.aliyun.com/#/ticket/createIndex)

## 代码许可
MIT许可证，参见LICENSE文件。