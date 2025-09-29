# xbot.web 模块

## 描述

对 web 网页进行各式操作，如打开网页、关闭网页。

## 方法

### `create(url, mode='cef', load_timeout=20, stop_if_timeout=False, silent_running=False, executable_path=None, arguments=None)`

打开网页。

**参数：**
- `url`：目标网址
- `mode`：浏览器类型，默认为 `'cef'`
- `load_timeout`：等待加载超时时间，默认 20 秒
- `stop_if_timeout`：网页加载超时是否停止加载网页，默认为 `False`
- `silent_running`：是否开启运行时不抢占鼠标键盘，默认为 `False`
- `executable_path`：浏览器执行文件路径，默认为 `None`
- `arguments`：命令行参数，默认为 `None`

**支持的浏览器类型：**

| mode 值 | 解释 |
|---------|------|
| `'cef'` | 影刀浏览器（默认值） |
| `'chrome'` | Google Chrome 浏览器 |
| `'ie'` | Internet Explorer 浏览器 |
| `'edge'` | Microsoft Edge 浏览器 |
| `'360se'` | 360 安全浏览器 |
| 自定义值 | 自定义浏览器 / 指纹浏览器 |

**返回值：**
- `WebBrowser`：返回打开的网页对象

**示例：**
```python
from xbot import web

def main(args):
    web_object = web.create('www.baidu.com', 'chrome', load_timeout=20)
```

**执行逻辑：** 使用 Chrome 浏览器打开百度官网

---

### `get(title=None, url=None, mode='cef', load_timeout=20, use_wildcard=False, stop_if_timeout=False, open_page=False, page_url=None, silent_running=False)`

根据网址或标题获取网页。

**参数：**
- `title`：网页标题
- `url`：网址
- `mode`：浏览器类型，默认为 `'cef'`
- `load_timeout`：等待加载超时时间，默认 20 秒
- `use_wildcard`：是否使用通配符方式匹配，默认为 `False`
- `stop_if_timeout`：网页加载超时是否停止加载网页，默认为 `False`
- `open_page`：根据 url 或 title 匹配失败时，是否打开新的网页，默认为 `False`
- `page_url`：`open_page=True` 时，指定打开的网页地址
- `silent_running`：是否开启运行时不抢占鼠标键盘，默认为 `False`

**返回值：**
- `WebBrowser`：返回获取到的网页对象

**示例1 - 模糊匹配：**
```python
from xbot import web

def main(args):
    web_object = web.get('百度', None, 'chrome', load_timeout=20, use_wildcard=False)
```

**执行逻辑：** 使用模糊匹配在 Chrome 浏览器中查找标题开头为"百度"的网页对象

**示例2 - 通配符匹配：**
```python
from xbot import web

def main(args):
    web_object = web.get('百度*', None, 'chrome', load_timeout=20, use_wildcard=True)
```

**执行逻辑：** 使用通配符在 Chrome 浏览器中查找标题开头为"百度"的网页对象

---

### `get_active(mode='cef', load_timeout=20, stop_if_timeout=False, silent_running=False)`

获取当前选中或激活的网页。

**参数：**
- `mode`：浏览器类型，默认为 `'cef'`
- `load_timeout`：等待加载超时时间，默认 20 秒
- `stop_if_timeout`：网页加载超时是否停止加载网页，默认为 `False`
- `silent_running`：是否开启运行时不抢占鼠标键盘，默认为 `False`

**返回值：**
- `WebBrowser`：返回获取到的网页对象

**示例：**
```python
from xbot import web

def main(args):
    web_object = web.get_active('chrome', load_timeout=20)
```

**执行逻辑：** 获取 Chrome 浏览器当前激活的网页对象

---

### `get_all(mode='cef', title=None, url=None, use_wildcard=False, silent_running=False)`

获取所有网页。

**参数：**
- `mode`：浏览器类型，默认为 `'cef'`
- `title`：网页标题
- `url`：网址
- `use_wildcard`：是否使用通配符方式匹配，默认为 `False`
- `silent_running`：是否开启运行时不抢占鼠标键盘，默认为 `False`

**返回值：**
- `List[WebBrowser]`：返回网页对象列表

**示例：**
```python
from xbot import web

def main(args):
    web_objects = web.get_all('chrome')
```

**执行逻辑：** 获取 Chrome 浏览器当前打开的全部网页对象

---

### `get_cookies(mode='cef', url=None, name=None, domain=None, path=None)`

获取浏览器 Cookie 信息。

**参数：**
- `mode`：浏览器类型，默认为 `'cef'`
- `url`：根据给定的 url 找到相应的 cookie，如：`url='https://www.yingdao.com'`
- `name`：根据 cookie 的 name 来筛选 cookie
- `domain`：根据 cookie 的 domain 来筛选 cookie
- `path`：根据 cookie 的 path 来筛选 cookie

**返回值：**
- `List[dict]`：返回筛选到的 cookie 列表，列表项为字典

**示例：**
```python
from xbot import web

def main(args):
    get_explorer_cookie('cef')
    pass

def get_explorer_cookie(mode):
    # 获取浏览器 cookie
    cookie_list = web.get_cookies(mode)
    print(cookie_list)
    for cookie in cookie_list:
        print(cookie['name'] + '    ' + cookie['value'])
```

**执行逻辑：** 获取影刀浏览器下的所有 cookie → 打印筛选出的 cookie 所有字段

---

### `get_cookies_v2(mode='cef', name=None, url=None, domain=None, path=None, partition_key=None, secure=None, session=None)`

获取浏览器 Cookie 信息，支持 PartitionKey。

**参数：**
- `mode`：浏览器类型，默认为 `'cef'`
- `name`：根据给定的 name 筛选 cookie
- `url`：根据给定的 URL 筛选 cookie
- `domain`：根据 cookie 的 domain 来筛选 cookie
- `path`：根据 cookie 的 path 来筛选 cookie
- `partition_key`：根据 cookie 的 partition key 来筛选 cookie
- `secure`：是否获取 secure Cookie 集合
- `session`：是否获取会话 Cookie 集合

**支持的浏览器类型：**
- `'cef'`：影刀浏览器（默认值）
- `'chrome'`：Google Chrome 浏览器
- `'ie'`：Internet Explorer 浏览器
- `'edge'`：Microsoft Edge 浏览器
- `'360se'`：360 安全浏览器
- `'firefox'`：FireFox 浏览器
- 自定义值：自定义浏览器 / 指纹浏览器

**返回值：**
- `List[dict]`：返回筛选到的 cookie 列表，列表项为字典

**示例：**
```python
from xbot import web

def main(args):
    get_explorer_cookie('chrome')
    pass

def get_explorer_cookie(mode):
    # 获取浏览器 cookie
    cookie_list = web.get_cookies(mode, partition_key="https://taobao.com")
    print(cookie_list)
    for cookie in cookie_list:
        print(cookie['name'] + '    ' + cookie['value'])
```

**执行逻辑：** 获取 Chrome 浏览器中 PartitionKey 为 `'https://taobao.com'` 的 cookie 信息

---

### `set_cookie(url, mode='cef', name=None, value=None, sessionCookie=True, expires=100, domain=None, path=None, httpOnly=False, secure=False)`

设置浏览器 Cookie 信息。

**参数：**
- `url`：根据给定的 URL 设置 cookie，该参数必填
- `mode`：浏览器类型，默认为 `'cef'`
- `name`：根据给定的 name 设置 cookie，该参数必填
- `value`：根据给定的 value 设置 cookie
- `sessionCookie`：默认为 `True`，设置为会话 cookie
- `expires`：持久化 cookie 需要设置有效期（秒），默认 100 秒
- `domain`：根据给定的 domain 设置 cookie
- `path`：根据给定的 path 设置 cookie
- `httpOnly`：设置该 cookie 是否被标记为 HttpOnly，默认为 `False`
- `secure`：设置该 cookie 是否被标记为 Secure，默认为 `False`

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    web.set_cookie('https://www.baidu.com', mode="chrome", name="test")
    pass
```

**执行逻辑：** 设置 Chrome 浏览器 `https://www.baidu.com` 网址 `name="test"` 的 cookie

---

### `remove_cookie(url, name, mode='cef')`

移除通过 cookie url、cookie name 指定的 cookie。

**参数：**
- `url`：将被移除的 cookie url
- `name`：将被移除的 cookie 名称
- `mode`：浏览器类型，默认为 `'cef'`

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    web.remove_cookie('https://www.baidu.com', 'BIDUPSID', 'edge')
    pass
```

**执行逻辑：** 移除 Edge 浏览器的"BIDUPSID"百度网站的 cookie 信息

---

### `close_all(mode='cef', task_kill=False)`

关闭所有网页。

**参数：**
- `mode`：浏览器类型，默认为 `'cef'`
- `task_kill`：是否终止浏览器进程，默认为 `False`

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    web.close_all('chrome')
```

**执行逻辑：** 关闭 Chrome 浏览器当前打开的全部网页

---

### `handle_save_dialog(file_folder, dialog_result='ok', mode='cef', *, file_name=None, wait_appear_timeout=20, focus_timeout=600)`

处理网页下载对话框。

**参数：**
- `file_folder`：文件保存路径
- `dialog_result`：点击下载对话框中按钮，`'ok'` 为确认下载，`'cancel'` 为取消下载
- `mode`：浏览器类型，默认为 `'cef'`
- `file_name`：保存文件名，默认为 `None`（为下载资源生成不重复的文件名）
- `wait_appear_timeout`：等待对话框出现超时时间，默认 20 秒
- `focus_timeout`：焦点超时时间，默认 600 毫秒

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    web.handle_save_dialog('D:\\', 'ok', 'chrome', file_name='123.txt', wait_appear_timeout=20)
```

**执行逻辑：** 在 Chrome 浏览器中处理下载对话框，并将目标文件重命名为"123.txt"并保存到 D 盘根目录下

---

### `handle_upload_dialog(filename, dialog_result='ok', mode='cef', *, wait_appear_timeout=20)`

处理网页上传对话框。

**参数：**
- `filename`：文件路径
- `dialog_result`：点击上传对话框中按钮，`'ok'` 为确认上传，`'cancel'` 为取消上传
- `mode`：浏览器类型，默认为 `'cef'`
- `wait_appear_timeout`：等待对话框出现超时时间，默认 20 秒

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    web.handle_upload_dialog('D:\\123.txt', 'ok', 'chrome', wait_appear_timeout=20)
```

**执行逻辑：** 在 Chrome 浏览器中处理网页上传对话框，上传 `D:\123.txt` 文件

## 浏览器支持

| 浏览器类型 | mode 值 | 说明 |
|------------|---------|------|
| 影刀浏览器 | `'cef'` | 默认浏览器 |
| Google Chrome | `'chrome'` | 需要安装 Chrome |
| Internet Explorer | `'ie'` | Windows 系统自带 |
| Microsoft Edge | `'edge'` | Windows 10+ 系统自带 |
| 360 安全浏览器 | `'360se'` | 需要安装 360 安全浏览器 |
| FireFox | `'firefox'` | 需要安装 FireFox |
| 自定义浏览器 | 自定义值 | 根据配置文件设置 |
