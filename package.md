# Package 模块

## 描述

package 模块用于获取各类元素（网页元素、软件元素及图像元素）及对资源文件进行读写等操作。

## 模块组成

package 模块内部一共由三类对象组成：
- 元素选择器（selector）
- 图像选择器（image_selector）
- 资源文件对象（resources）

## 元素选择器（selector）

根据元素名称返回元素选择器对象。元素选择器指的是在元素库中捕获的网页元素或软件元素。

### 方法

#### `selector(name)`

**参数：**
- `name`：选择器名称，即元素库中元素的名称

**返回值：**
- `Selector`：元素选择器对象，即通过元素名称所指定的元素

**示例：**
```python
from .package import *

def main(args):
    # 这里"百度一下"指的是元素库中名为"百度一下"的网页元素
    selector = package.selector('百度一下')
    print(selector)
```

## 图像选择器（image_selector）

根据图像库中图像元素的名称返回图像选择器对象。

### 方法

#### `image_selector(name)`

**参数：**
- `name`：图像选择器名称，即图像库中图像元素的名称

**返回值：**
- `ImageSelector`：图像选择器对象，即通过图像元素名称所指定的元素

**示例：**
```python
from .package import *

def main(args):
    selector = package.image_selector('图像1')  # 这里"图像1"指的是图像库中名称为"图像1"的图像元素
```

## 资源文件对象（resources）

通过调用 `package.resources` 获取资源文件对象以便对资源文件进行读写操作。

### 方法

#### `get_text(filename, encoding='utf-8')`

获取资源文件的文本内容。

**参数：**
- `filename`：资源文件名
- `encoding`：读取文件时的编码格式，若不传入，则默认以 utf-8 的格式读取

**返回值：**
- `str`：返回资源文件的文本内容

**示例：**
```python
from . import package

def main(args):
    text = package.resources.get_text('123.txt')
    print(text)
```

#### `get_bytes(filename)`

获取资源文件的二进制信息。

**参数：**
- `filename`：资源文件名

**返回值：**
- `byte`：返回资源文件的二进制信息

**示例：**
```python
from . import package

def main(args):
    value = package.resources.get_bytes('123.txt')  # 输出结果将以二进制的形式返回
    print(value)
```

#### `copy_to(filename, dest_filename)`

将资源文件的内容拷贝到目标文件中。

**参数：**
- `filename`：资源文件名
- `dest_filename`：资源文件内容最终拷贝到的位置（为文件绝对路径，如 "D:\123.txt"）

**返回值：**
- 无

**示例：**
```python
from . import package

def main(args):
    package.resources.copy_to('123.txt', 'D:\\aaa.txt')
```

#### `add_to_clipboard(filenames)`

将资源文件添加到剪切板。

**参数：**
- `filenames`：资源文件名列表（一定要注意！），如 `['123.txt', '234.xml']`

**返回值：**
- 无

**示例：**
```python
from . import package

def main(args):
    package.resources.add_to_clipboard(['123.txt', '234.xml'])
```
