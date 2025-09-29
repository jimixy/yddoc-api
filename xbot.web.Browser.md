# xbot.web.Browser 模块

## 描述

对网页元素、网页进行的各种处理，如网页激活、获取网页标题、网页重新加载、取消网页加载等。

## 类

### `WebBrowser`

网页浏览器类，用于操作网页的各种功能。

## 方法

### 网页信息获取

#### `get_url()`

获取网址。

**参数：**
- 无

**返回值：**
- `str`：返回网页地址

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    url = browser.get_url()
```

**执行逻辑：** 获取已打开的网页对象 → 获取url地址

---

#### `get_title()`

获取标题。

**参数：**
- 无

**返回值：**
- `str`：返回网页标题

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    title = browser.get_title()
```

**执行逻辑：** 获取已打开的网页对象 → 获取标题

---

#### `get_text()`

获取网页的文本内容。

**参数：**
- 无

**返回值：**
- `str`：返回网页文本内容

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    text = browser.get_text()
```

**执行逻辑：** 获取已打开的网页对象 → 获取当前激活网页的文本内容

---

#### `get_html()`

获取网页的html。

**参数：**
- 无

**返回值：**
- `str`：返回网页的html

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    html = browser.get_html()
```

**执行逻辑：** 获取已打开的网页对象 → 获取当前激活网页的html

---

### 网页导航

#### `activate()`

激活目标网页。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    browser.activate()
```

**执行逻辑：** 获取标题为百度的网页对象 → 激活该网页

---

#### `navigate(url, load_timeout=20)`

跳转到新网页。

**参数：**
- `url`：新网页地址
- `load_timeout`：等待加载超时时间，默认超时时间20s，若超时未加载完毕则抛出UIAError异常

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    browser.navigate('www.taobao.com')
```

**执行逻辑：** 获取标题为百度的网页对象 → 将该网页跳转到淘宝网页

---

#### `go_back(load_timeout=20)`

网页后退。

**参数：**
- `load_timeout`：等待加载超时时间，默认超时时间20s，若超时未加载完毕则抛出UIAError异常

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('淘宝', None, 'chrome')
    browser.go_back()
```

**执行逻辑：** 获取标题为淘宝的网页并后退

---

#### `go_forward(load_timeout=20)`

网页前进。

**参数：**
- `load_timeout`：等待加载超时时间，默认超时时间20s，若超时未加载完毕则抛出UIAError异常

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    browser.go_forward()
```

**执行逻辑：** 获取标题为百度的网页并前进

---

### 网页加载控制

#### `reload(ignore_cache=False, load_timeout=20)`

网页重新加载。

**参数：**
- `ignore_cache`：是否忽略缓存，默认为 `False`（不忽略）
- `load_timeout`：等待加载超时时间，默认超时时间20s，若超时未加载完毕则抛出UIAError异常

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    browser.reload(True)
```

**执行逻辑：** 获取标题为百度的网页不忽略缓存重新加载

---

#### `stop_load()`

网页停止加载。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    browser.stop_load()
```

**执行逻辑：** 获取标题为百度的网页并停止加载

---

#### `is_load_completed()`

判断网页是否加载完成。

**参数：**
- 无

**返回值：**
- `bool`：返回网页是否加载完成，完成返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get('百度', None, 'chrome')
    is_load_completed = browser.is_load_completed()
```

**执行逻辑：** 获取标题为百度的网页并判断其是否加载完成

---

#### `wait_load_completed(timeout=20)`

等待网页加载完成。

**参数：**
- `timeout`：等待超时时间，默认20秒

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.wait_load_completed()
```

**执行逻辑：** 获取当前激活的窗口并等待其加载完成

---

#### `close()`

关闭网页。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.close()
```

**执行逻辑：** 获取当前激活的窗口并关闭

---

### JavaScript 操作

#### `execute_javascript(code, argument=None)`

在网页元素上执行JS脚本。

**参数：**
- `code`：要执行的JS脚本，必须为javascript函数形式
- `argument`：要传入到JS函数中的参数，必须为字符串，如果需要传入其他类型可以先将其转为JSON字符串形式

**返回值：**
- `Any`：返回JS脚本执行结果

**示例：**
```python
from xbot import web, print

def main(args):
    page = web.get_active()
    code = """
    function (context, args) {
            // context为null
            // args表示输入的参数
            return "hello " + args;
    }
    """
    js_result = page.execute_javascript(code, 'james')
    print(js_result) # 打印'hello james'
```

**执行逻辑：** 获取当前激活的网页 → 在此页面上执行一段JS函数 → 获取并打印其返回值

---

### 网页滚动

#### `scroll_to(location='bottom', behavior='instant', top=0, left=0)`

鼠标滚动网页。

**参数：**
- `location`：网页要滚动到的位置，可以选择 `'bottom'`（滚动到底部）、`'top'`（滚动到顶部）或 `'point'`（滚动到指定位置），默认滚动到底部
- `behavior`：网页滚动效果，可以设置 `'instant'`（瞬间滚动）或 `'smooth'`（平滑滚动），默认值为 `'instant'`（瞬间滚动）
- `top`：滚动到指定位置的纵坐标
- `left`：滚动到指定位置的横坐标

**返回值：**
- 无

**示例1：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.scroll_to(location='bottom', behavior='smooth')
```

**执行逻辑：** 获取当前激活的网页 → 使用鼠标平滑滚动网页至底部

**示例2：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.scroll_to(location='point', behavior='smooth', top=100, left=100)
```

**执行逻辑：** 获取当前激活的网页 → 使用鼠标平滑滚动网页至 top:100，left:100 的位置

---

### 对话框处理

#### `handle_javascript_dialog(dialog_result='ok', text=None, wait_appear_timeout=20)`

处理网页对话框。

**参数：**
- `dialog_result`：点击下载对话框中按钮，`'ok'`为确认下载，`'cancel'`为取消下载
- `text`：输入网页对话框的内容，可为 `None`
- `wait_appear_timeout`：等待对话框出现超时时间，默认20s，如果下载对话框加载超时则抛出UIAError的异常

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.handle_javascript_dialog('ok', text='helloword')
```

**执行逻辑：** 获取当前激活的网页 → 处理当前网页的对话框，并将 helloword 填写到对话框中

---

#### `get_javascript_dialog_text(wait_appear_timeout=20)`

获取网页对话框内容(Chrome不支持此操作)。

**参数：**
- `wait_appear_timeout`：等待对话框出现超时时间，默认20s，如果下载对话框加载超时则抛出UIAError的异常

**返回值：**
- `str`：返回网页对话框的内容

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    content = browser.get_javascript_dialog_text()
```

**执行逻辑：** 获取当前激活的网页 → 获取当前激活网页中的对话框内容

---

### 网络监听

#### `start_monitor_network()`

开始监听网页请求(Chrome，ie不支持此操作)。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.start_monitor_network()
    browser.reload()
    network_result_list = browser.get_responses(url='baidu', use_wildcard=False, resource_type='All')
    browser.stop_monitor_network()
```

**执行逻辑：** 获取当前激活的网页 → 开始监听当前激活网页请求 → 网页刷新 → 获取请求结果 → 停止监听网页请求

---

#### `stop_monitor_network()`

停止监听网页请求(Chrome，ie不支持此操作)。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.start_monitor_network()
    browser.reload()
    network_result_list = browser.get_responses(url='baidu', use_wildcard=False, resource_type='All')
    browser.stop_monitor_network()
```

**执行逻辑：** 获取当前激活的网页 → 开始监听当前激活网页请求 → 网页刷新 → 获取请求结果 → 停止监听网页请求

---

#### `get_responses(url, use_wildcard=False, resource_type='All')`

获取网页请求结果(Chrome，ie不支持此操作)。

**参数：**
- `url`：资源路径Url
- `use_wildcard`：是否使用通配符方式匹配，默认为 `False`（模糊匹配，如果为True则使用通配符方式匹配）
- `resource_type`：要过滤的网页请求结果类型，默认为 `'All'`。包括All, XHR, Script, Style sheet, Image, Media, Font, Document, WebSocket, Manifest, TextTrack, Fetch, EventSource, Other

**返回值：**
- `List[dict]`：返回网页请求结果列表，列表项为字典

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    browser.start_monitor_network()
    browser.reload()
    network_result_list = browser.get_responses(url='baidu', use_wildcard=False, resource_type='All')
    browser.stop_monitor_network()
```

**执行逻辑：** 获取当前激活的网页 → 开始监听当前激活网页请求 → 网页刷新 → 获取请求结果 → 停止监听网页请求

---

### 元素等待

#### `wait_appear(selector_or_element, timeout=20)`

等待网页元素出现。

**参数：**
- `selector_or_element`：要查找的选择器，支持两种格式——str类型（查找元素库中的元素）和Selector类型（在流程中已经获取过的网页元素对象）
- `timeout`：等待网页元素出现超时时间，默认超时时间20s

**返回值：**
- `bool`：返回网页元素是否出现，出现返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    is_appear = browser.wait_appear('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 等待当前激活的网页中出现与元素选择器"百度一下"匹配的网页元素出现

---

#### `wait_disappear(selector_or_element, timeout=20)`

等待网页元素消失。

**参数：**
- `selector_or_element`：要查找的选择器，支持两种格式——str类型（查找元素库中的元素）和Selector类型（在流程中已经获取过的网页元素对象）
- `timeout`：等待网页元素出现超时时间，默认超时时间20s

**返回值：**
- `bool`：返回网页元素是否消失结果，消失返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    is_disappear = browser.wait_disappear('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 等待当前激活的网页中出现与元素选择器"百度一下"匹配的网页元素消失

---

### 元素查找

#### `find(selector, timeout=20)`

在当前网页中获取与选择器匹配的网页元素对象。

**参数：**
- `selector`：要查找的选择器，支持两种格式——str类型（查找元素库中的元素）和Selector类型（在流程中已经获取过的网页元素对象）
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `WebElement`：返回目标网页元素对象

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    web_element = browser.find('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与元素选择器"百度一下"匹配的元素并返回第一个

---

#### `find_all(selector, timeout=20)`

在当前网页中获取与选择器匹配的相似网页元素列表。

**参数：**
- `selector`：要查找的选择器，支持两种格式——str类型（查找元素库中的元素）和Selector类型（在流程中已经获取过的网页元素对象）
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `List[WebElement]`：返回和目标元素相似网页元素列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    list_web_element = browser.find_all('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与元素选择器"百度一下"匹配的所有元素的列表

---

#### `find_by_css(css_selector, timeout=20)`

在当前网页中获取符合CSS选择器的网页元素对象。

**参数：**
- `css_selector`：CSS选择器，字符串类型
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `WebElement`：返回网页元素对象

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    web_element = browser.find_by_css('#su')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取符合id为su的网页元素并返回第一个

---

#### `find_all_by_css(css_selector, timeout=20)`

在当前网页中获取符合CSS选择器的网页元素列表。

**参数：**
- `css_selector`：CSS选择器，字符串类型
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `List[WebElement]`：返回相似网页元素列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    list_web_element = browser.find_all_by_css('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与CSS选择器"百度一下"匹配的全部网页元素列表

---

#### `find_by_xpath(xpath_selector, timeout=20)`

在当前网页中获取符合Xpath选择器的网页元素对象。

**参数：**
- `xpath_selector`：xpath字符串语法
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `WebElement`：返回网页元素对象

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    web_element = browser.find_by_xpath('//*[@id="su"]')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与Xpath选择器'//*[@id="su"]'匹配的网页元素并返回第一个

---

#### `find_all_by_xpath(xpath_selector, timeout=20)`

在当前网页中获取符合Xpath选择器的网页元素列表。

**参数：**
- `xpath_selector`：xpath字符串语法
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `List[WebElement]`：返回相似网页元素列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    list_web_element = browser.find_all_by_xpath('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与Xpath选择器"百度一下"匹配的全部网页元素集合

---

### 元素状态判断

#### `is_element_displayed(selector)`

网页元素是否可见。

**参数：**
- `selector`：要查找的选择器，支持两种格式——str类型（查找元素库中的元素）和Selector类型（在流程中已经获取过的网页元素对象）

**返回值：**
- `bool`：返回网页元素是否可见，可见返回 `True`，反之返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    is_displayed = browser.is_element_displayed('百度一下')
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中判断与元素选择器"百度一下"匹配的网页元素是否可见

---

### 表格数据提取

#### `extract_table(table_selector, exclude_thead=False, timeout=20)`

获取选择器对应表格数据。

**参数：**
- `table_selector`：要查找的表格选择器，支持两种格式——str类型（查找元素库中的数据表格元素）和TableSelector类型（在流程中已经获取过的数据表格元素对象）
- `exclude_thead`：表格数据抓取多页时，只保留第一页抓取结果的表头。默认 `False`，结果保留每页抓取的结果的表头（仅对表格元素生效）
- `timeout`：获取网页相似元素列表超时时间，默认超时时间20s，匹配元素超时未找到则抛出UAIError异常

**返回值：**
- `List`：返回网页上与目标元素相似的元素列表

**示例1 - 保留每页表头：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    # 整表抓取多页时，结果保留每页抓取结果的表头（仅对表格元素生效）
    table_list = browser.extract_table('数据表格', exclude_thead=False)
```

**示例2 - 只保留第一页表头：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    # 整表抓取多页时，结果只保留第一页抓取结果的表头（仅对表格元素生效）
    table_list = browser.extract_table('数据表格', exclude_thead=True)
```

**执行逻辑：** 获取当前激活的网页 → 在当前激活的网页中获取与表格选择器"数据表格"匹配的元素列表

## 功能分类总结

| 功能类别 | 方法 | 说明 |
|----------|------|------|
| **网页信息获取** | `get_url()` | 获取网址 |
| | `get_title()` | 获取标题 |
| | `get_text()` | 获取文本内容 |
| | `get_html()` | 获取HTML内容 |
| **网页导航** | `activate()` | 激活网页 |
| | `navigate()` | 跳转到新网页 |
| | `go_back()` | 网页后退 |
| | `go_forward()` | 网页前进 |
| **网页加载控制** | `reload()` | 重新加载 |
| | `stop_load()` | 停止加载 |
| | `is_load_completed()` | 判断是否加载完成 |
| | `wait_load_completed()` | 等待加载完成 |
| | `close()` | 关闭网页 |
| **JavaScript操作** | `execute_javascript()` | 执行JS脚本 |
| **网页滚动** | `scroll_to()` | 滚动网页 |
| **对话框处理** | `handle_javascript_dialog()` | 处理对话框 |
| | `get_javascript_dialog_text()` | 获取对话框内容 |
| **网络监听** | `start_monitor_network()` | 开始监听网络 |
| | `stop_monitor_network()` | 停止监听网络 |
| | `get_responses()` | 获取请求结果 |
| **元素等待** | `wait_appear()` | 等待元素出现 |
| | `wait_disappear()` | 等待元素消失 |
| **元素查找** | `find()` | 查找单个元素 |
| | `find_all()` | 查找所有元素 |
| | `find_by_css()` | CSS选择器查找 |
| | `find_all_by_css()` | CSS选择器查找所有 |
| | `find_by_xpath()` | XPath选择器查找 |
| | `find_all_by_xpath()` | XPath选择器查找所有 |
| **元素状态判断** | `is_element_displayed()` | 判断元素是否可见 |
| **表格数据提取** | `extract_table()` | 提取表格数据 |

## 注意事项

1. **浏览器兼容性**：某些功能（如网络监听、对话框获取）在Chrome和IE中可能不支持
2. **超时处理**：大部分方法都有超时参数，超时后会抛出UIAError异常
3. **选择器支持**：元素查找方法支持多种选择器格式，包括字符串、CSS选择器、XPath等
4. **异步加载**：网页加载相关方法需要等待页面完全加载完成才能正常使用
