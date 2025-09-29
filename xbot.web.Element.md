# xbot.web.Element 模块

## 描述

对网页元素进行处理，如获取相似网页元素、查找目标元素父/子元素、点击元素等。

## 类

### `WebElement`

网页元素类，用于操作网页中的各种元素。

## 方法

### 元素关系操作

#### `parent()`

获取当前元素的父元素。

**参数：**
- 无

**返回值：**
- `WebElement`：返回当前元素的父元素

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    web_element = browser.find('百度一下')
    parent_element = web_element.parent()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 获取该对象的父元素

---

#### `children()`

获取当前元素的所有子元素。

**参数：**
- 无

**返回值：**
- `List[WebElement]`：返回当前元素的所有子元素

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    web_element = browser.find('百度一下')
    children_elements = web_element.children()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 获取该对象的子元素列表

---

#### `child_at(index)`

获取指定位置的子元素。

**参数：**
- `index`：子元素的位置索引，从0开始计数

**返回值：**
- `WebElement`：返回指定位置的子元素

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    web_element = browser.find('左上角的菜单栏')
    child_element = web_element.child_at(0)
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"左上角的菜单栏"的网页元素对象 → 获取该对象子元素下的第一个子元素

---

#### `previous_sibling()`

获取上一个并列的兄弟元素。

**参数：**
- 无

**返回值：**
- `WebElement`：返回上一个并列的兄弟元素

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    web_element = browser.find('左上角的菜单栏')
    child_element = web_element.previous_sibling()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"左上角的菜单栏"的网页元素对象 → 获取该对象上一个并列的兄弟元素

---

#### `next_sibling()`

获取下一个并列的兄弟元素。

**参数：**
- 无

**返回值：**
- `WebElement`：返回下一个并列的兄弟元素

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    web_element = browser.find('左上角的菜单栏')
    child_element = web_element.next_sibling()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"左上角的菜单栏"的网页元素对象 → 获取该对象下一个并列的兄弟元素

---

### 鼠标操作

#### `click(button='left', simulative=True, keys='none', delay_after=1, move_mouse=False, anchor=None)`

单击当前网页元素。

**参数：**
- `button`：要点击的鼠标按键，可传入 `'left'` 或 `'right'`，默认为 `'left'`（鼠标左键）
- `simulative`：是否模拟人工点击，默认为 `True`（模拟人工点击）
- `move_mouse`：是否显示鼠标移动轨迹，默认为 `True`，显示鼠标移动轨迹
- `keys`：点击鼠标时的键盘辅助按钮，可用辅助按键有——none、alt、ctrl、shift 和 win，默认为 `'none'`
- `delay_after`：执行成功后延迟时间，默认延迟 1s
- `anchor`：锚点，鼠标点击元素的位置以及偏移量元组，可为 `None`，默认值为 `None`（点击目标中心且无偏移量）

**锚点参数结构：**
- `sudoku_part`：鼠标点击的位置，默认点击中心
- `offset_x`：鼠标位置的水平偏移量
- `offset_y`：鼠标位置的垂直偏移量

**锚点位置选项：**

| 参数值 | 解释 |
|--------|------|
| `'topLeft'` | 左上角 |
| `'topCenter'` | 上中部 |
| `'topRight'` | 右上角 |
| `'middleLeft'` | 左中部 |
| `'middleCenter'` | 中心 |
| `'middleRight'` | 右中部 |
| `'bottomLeft'` | 左下角 |
| `'bottomCenter'` | 下中部 |
| `'bottomRight'` | 右下角 |
| `'random'` | 随机位置 |

**返回值：**
- 无

**示例1：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').click(button='left', move_mouse=True)
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 鼠标模拟人工点击该元素

**示例2：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').click(button='left', move_mouse=True, anchor=('topLeft', 100, 100))
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 鼠标左键在元素的左上角水平偏移100垂直偏移100的位置单击

---

#### `dblclick(simulative=True, delay_after=1, move_mouse=False, anchor=None)`

双击当前网页元素。

**参数：**
- `simulative`：是否模拟人工点击，默认为 `True`（模拟人工点击）
- `move_mouse`：是否显示鼠标移动轨迹，默认为 `True`，显示鼠标移动轨迹
- `delay_after`：执行成功后延迟时间，默认延迟 1s
- `anchor`：锚点，鼠标点击元素的位置以及偏移量元组，可为 `None`，默认值为 `None`（点击目标中心且无偏移量）

**锚点参数结构：**
- `sudoku_part`：鼠标双击的位置，默认双击中心
- `offset_x`：鼠标位置的水平偏移量
- `offset_y`：鼠标位置的垂直偏移量

**锚点位置选项：** 同 `click()` 方法

**返回值：**
- 无

**示例1：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').dblclick(move_mouse=True, anchor=('topLeft', 100, 100))
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 鼠标在元素的左上角水平偏移100垂直偏移100的位置双击

**示例2：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').dblclick(move_mouse=True)
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"百度一下"的网页元素对象 → 鼠标左键双击该元素

---

#### `hover(simulative=True, delay_after=1)`

鼠标悬停在当前元素。

**参数：**
- `simulative`：是否模拟人工悬停，默认为 `True`（模拟人工悬停）
- `delay_after`：执行成功后延迟时间，默认延迟 1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('输入框').hover()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 将鼠标悬停在元素名称为"输入框"的元素对象上

---

#### `drag_to(simulative=True, behavior='smooth', top=0, left=0, delay_after=1)`

拖拽网页元素到指定位置。

**参数：**
- `simulative`：是否模拟人工点击，默认为 `True`（模拟人工点击）
- `behavior`：网页滚动效果，可以设置 `'instant'`（瞬间滚动）或 `'smooth'`（平滑滚动），默认值为 `'instant'`（瞬间滚动）
- `top`：滚动到指定位置的纵坐标
- `left`：滚动到指定位置的横坐标
- `delay_after`：指令执行成功后延迟执行时间，默认值为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('可移动元素').drag_to(simulative=True, behavior='smooth', top=100, left=100)
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"可移动元素"的网页元素，并模拟人工拖拽元素到 top:100，left:100 位置

---

### 输入操作

#### `input(text, simulative=True, append=False, contains_hotkey=False, send_key_delay=50, focus_timeout=1000, delay_after=1, anchor=None)`

填写网页输入框。

**参数：**
- `text`：需要填写到输入框中的文本内容
- `simulative`：是否模拟人工点击，默认为 `True`（模拟人工点击）
- `append`：是否追加输入，追加输入会保留输入框中原有内容，默认为 `False`（非追加写入）
- `contains_hotkey`：输入内容是否包含快捷键，该选项只有在模拟人工输入时起效，默认为 `False`（不包含快捷键）
- `send_key_delay`：两次按键之间的时间间隔(对影刀浏览器该参数无效)，默认为50ms
- `delay_after`：执行成功后延迟时间，默认延迟 1s
- `anchor`：锚点，鼠标点击元素的位置以及偏移量元组，可为 `None`，默认值为 `None`（点击目标中心且无偏移量）
- `focus_timeout`：焦点超时时间(获取焦点和输入操作的间隔)，默认1000毫秒

**锚点参数结构：**
- `sudoku_part`：鼠标悬停的位置，默认悬停在中心
- `offset_x`：鼠标位置的水平偏移量
- `offset_y`：鼠标位置的垂直偏移量

**锚点位置选项：**

| 参数值 | 解释 |
|--------|------|
| `'topLeft'` | 悬停左上角 |
| `'topCenter'` | 悬停在上中部 |
| `'topRight'` | 悬停在右上角 |
| `'middleLeft'` | 悬停在左中部 |
| `'middleCenter'` | 悬停在中心 |
| `'middleRight'` | 悬停在右中部 |
| `'bottomLeft'` | 悬停左下角 |
| `'bottomCenter'` | 悬停在下中部 |
| `'bottomRight'` | 悬停在右下角 |

**返回值：**
- 无

**示例1：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    input_element = browser.find('输入框')
    input_element.input('影刀')
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"输入框"的网页元素对象 → 将"影刀"填写到元素中

**示例2：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    input_element = browser.find('输入框')
    input_element.input('hello world', anchor=('topLeft', 100, 100))
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"输入框"的网页元素对象 → 鼠标在元素的左上角水平偏移100垂直偏移100的位置单击，然后将"影刀"填写到元素中

---

#### `clipboard_input(text, append=False, delay_after=1, anchor=None, focus_timeout=1000)`

通过剪切板填写网页输入框(可有效避免输入法问题)。

**参数：**
- `text`：需要填写到输入框中的文本内容
- `append`：是否追加输入，追加输入会保留输入框中原有内容，默认为 `False`（非追加写入）
- `delay_after`：执行成功后延迟时间，默认延迟 1s
- `anchor`：锚点，鼠标点击元素的位置以及偏移量元组，可为 `None`，默认值为 `None`（点击目标中心且无偏移量）
- `focus_timeout`：焦点超时时间(获取焦点和输入操作的间隔)，默认1000毫秒

**锚点参数结构：** 同 `input()` 方法

**返回值：**
- 无

**示例1：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    input_element = browser.find('输入框')
    input_element.clipboard_input('hello world', append=True)
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"输入框"的网页元素对象 → 将"hello world"以剪切板的形式写入到元素中

**示例2：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    input_element = browser.find('输入框')
    input_element.clipboard_input('hello world', append=True, anchor=('topLeft', 100, 100))
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取元素名称为"输入框"的网页元素对象 → 鼠标在元素的左上角水平偏移100垂直偏移100的位置单击，然后将"hello world"以剪切板的形式写入到元素中

---

#### `focus()`

选中(激活)当前元素。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('输入框').focus()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 选中元素名称为"输入框"的元素对象，并选中该元素

---

### 内容获取

#### `get_text()`

获取当前网页元素的文本内容。

**参数：**
- 无

**返回值：**
- `str`：返回当前网页元素的文本内容

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    value = browser.find('输入框').get_text()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取名称为"输入框"的网页元素的文本内容

---

#### `get_html()`

获取当前网页元素的html内容。

**参数：**
- 无

**返回值：**
- `str`：返回当前网页元素的html内容

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    html = browser.find("百度一下").get_html()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取名称为"百度一下"的网页元素的html内容

---

#### `get_value()`

获取当前网页元素的值。

**参数：**
- 无

**返回值：**
- `str`：返回当前网页元素的值

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    value = browser.find('输入框').get_value()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 获取名称为"输入框"的网页元素的值

---

#### `set_value(value)`

设置当前网页元素的值。

**参数：**
- `value`：需要设置到网页元素上的文本值

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('输入框').set_value('hello world')
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 将名称为"输入框"的网页元素值设置为"hello world"

---

### 复选框操作

#### `check(mode='check', delay_after=1)`

设置网页复选框。

**参数：**
- `mode`：设置网页复选框的结果，可传入 `'check'`（选中）、`'uncheck'`（取消选中）或 `'toggle'`（反选），默认为 `'check'`（选中）
- `delay_after`：执行成功后延迟执行时间，默认时间为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('https://passport.baidu.com/v2/?login', 'chrome')
    browser.find('用户名登录').click()
    browser.find('下次自动登录').check('check')
```

**执行逻辑：** 通过Chrome浏览器打开百度登录网页 → 找到名称为"用户名登录"的网页复选框元素 → 设置该复选框元素为选中状态

---

#### `is_checked()`

判断网页复选框元素是否被选中。

**参数：**
- 无

**返回值：**
- `bool`：返回元素的选中状态，选中返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.xxx.com', 'chrome')
    is_checked = browser.find('复选框').is_checked()
```

**执行逻辑：** 通过Chrome浏览器打开xxx网页 → 找到名称为"复选框"的网页元素，判断该元素是否被选中

---

### 下拉框操作

#### `select(item, mode='fuzzy', delay_after=1)`

按选项内容设置单选网页下拉框元素。

**参数：**
- `item`：要设置的网页下拉框元素的某一项的文本内容
- `mode`：查找项的匹配模式，可以选择 `'fuzzy'`（模糊匹配）、`'exact'`（精准匹配）或 `'regex'`（正则匹配），默认是模糊匹配
- `delay_after`：执行成功后延迟执行时间，默认时间为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.taobao.com', 'chrome')
    browser.find('用户名').select('张三')
```

**执行逻辑：** 通过Chrome浏览器打开淘宝网页 → 找到名称为"用户名"的网页下拉框元素 → 使用精准匹配找到内容为"张三"并设置其为当前选中项

---

#### `select_multiple(items, mode='fuzzy', append=False, delay_after=1)`

按选项内容设置多选网页下拉框元素。

**参数：**
- `items`：要勾选的网页下拉框元素的列表
- `mode`：查找项的匹配模式，可以选择 `'fuzzy'`（模糊匹配）、`'exact'`（精准匹配）或 `'regex'`（正则匹配），默认是模糊匹配
- `append`：是否追加设置，默认值为 `False`（不追加）
- `delay_after`：执行成功后延迟执行时间，默认时间为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.xxx.com', 'chrome')
    browser.find('多选下拉框').select_multiple(['张三','李四', '王五'])
```

**执行逻辑：** 通过Chrome浏览器打开某网页 → 找到名称为"多选下拉框"的网页下拉框元素 → 使用精准匹配找到内容为"张三，李四，王五"并全部勾选

---

#### `select_by_index(index, delay_after=1)`

按下标设置单选网页下拉框元素。

**参数：**
- `index`：要设置的单选网页下拉框元素的位置，位置从0开始
- `delay_after`：执行成功后延迟执行时间，默认时间为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.taobao.com', 'chrome')
    browser.find('用户名').select_by_index(1)
```

**执行逻辑：** 通过Chrome浏览器打开淘宝网页 → 找到名称为"用户名"的网页下拉框元素 → 找到下拉框中下标为1的项并勾选

---

#### `select_multiple_by_index(indexes, append=False, delay_after=1)`

按下标设置多选网页下拉框元素。

**参数：**
- `indexes`：要设置的单选网页下拉框元素的位置列表，位置从0开始
- `append`：是否追加设置，默认值为 `False`（不追加）
- `delay_after`：执行成功后延迟执行时间，默认时间为1s

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.xxx.com', 'chrome')
    browser.find('多选下拉框').select_multiple_by_index([1,3,5])
```

**执行逻辑：** 通过Chrome浏览器打开某网页 → 找到名称为"多选下拉框"的网页下拉框元素 → 设置下拉框选项下标为1、3、5的项为选中状态

---

#### `get_select_options()`

获取网页下拉框的值。

**参数：**
- 无

**返回值：**
- `List[Tuple]`：返回下拉框值（选项，选项值，被选中状态）的列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.xxx.com', 'chrome')
    list_value = browser.find('下拉框').get_select_options()
```

**执行逻辑：** 通过Chrome浏览器打开xxx网页 → 找到名称为"下拉框"的网页下拉框元素并获取下拉框的值

---

#### `get_all_select_items()`

获取网页下拉框元素的全部下拉选项。

**参数：**
- 无

**返回值：**
- `List[str]`：返回网页下拉框全部下拉选项列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    element = browser.find('下拉框')
    values = element.get_all_select_items()
```

**执行逻辑：** 获取当前已打开的网页对象 → 找到名称为"下拉框"的网页元素 → 获取该元素的所有下拉选项

---

#### `get_selected_item()`

获取网页下拉框当前选中的项。

**参数：**
- 无

**返回值：**
- `List[str]`：返回网页下拉框当前全部选中项列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.get_active()
    element = browser.find('下拉框')
    values = element.get_selected_item()
```

**执行逻辑：** 获取当前已打开的网页对象 → 找到名称为"下拉框"的网页元素 → 获取该元素当前所有选中项

---

### 属性操作

#### `set_attribute(name, value)`

设置网页元素属性值。

**参数：**
- `name`：元素属性名称
- `value`：要设置的元素属性值

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').set_attribute('height', '100')
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素并设置该元素的height为100

---

#### `get_attribute(name)`

获取网页元素属性值。

**参数：**
- `name`：元素属性名称

**返回值：**
- `str`：返回网页元素目标属性的属性值

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    height = browser.find('百度一下').get_attribute('height')
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素并获取该元素的height属性值

---

#### `get_all_attributes()`

获取网页元素全部属性值。

**参数：**
- 无

**返回值：**
- `List[Tuple]`：返回目标网页元素的全部属性名与属性值的组合列表

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    list_tuple = browser.find('百度一下').get_all_attributes()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素并获取该元素的全部属性值

---

### 位置和状态

#### `get_bounding(to96dpi=True)`

获取网页元素的边框属性组合。

**参数：**
- `to96dpi`：是否需要将边框属性转换成dpi为96的对应属性值

**返回值：**
- `Tuple`：返回网页元素的边框属性组合，如('x', 'y', 'width', 'height')

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    list_tuple = browser.find('百度一下').get_bounding()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素并获取该元素的边框属性信息

---

#### `is_enabled()`

判断网页元素是否可用。

**参数：**
- 无

**返回值：**
- `bool`：返回元素的可用状态，可用返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    is_enabled = browser.find('百度一下').is_enabled()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素，判断该元素是否可用

---

#### `is_displayed()`

判断网页元素是否可见。

**参数：**
- 无

**返回值：**
- `bool`：返回元素的可见状态，可见返回 `True`，否则返回 `False`

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    is_displayed = browser.find('百度一下').is_displayed()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素，判断该元素是否可见

---

### 截图操作

#### `screenshot(folder_path, filename=None)`

对目标元素进行截图，并将图片进行保存。

**参数：**
- `folder_path`：元素截图后图片需要保存的路径
- `filename`：截图后图片保存后的名称，可为空，为空时会根据当前时间自动生成文件名称

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').screenshot('D:\\', filename='123.png')
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素然后对该元素截图，并将结果命名为"123.png"保存在D:下

---

#### `screenshot_to_clipboard()`

对目标元素进行截图，并将图片保存至剪切板。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import web

def main(args):
    browser = web.create('www.baidu.com', 'chrome')
    browser.find('百度一下').screenshot_to_clipboard()
```

**执行逻辑：** 通过Chrome浏览器打开百度网页 → 找到名称为"百度一下"的网页元素然后对该元素截图，并将结果添加到剪切板中

---

### 文件操作

#### `upload(file_names, clipboard_input=True, focus_timeout=1000, dialog_timeout=20)`

自动完成点击上传按钮、在文件选择对话框中输入待上传文件等系列操作。

**参数：**
- `file_names`：上传文件列表，比如 `[r"C:\test.txt",r"C:\text1.txt"]`
- `clipboard_input`：文件选择是否用剪切板输入，默认为 `True`（使用剪切板）
- `focus_timeout`：焦点超时时间(获取焦点和输入操作的间隔)，默认1000毫秒
- `dialog_timeout`：点击上传按钮后，等待文件选择框的最大时间，单位（秒）

**返回值：**
- 无

**示例：**
```python
import xbot
from xbot import print, sleep

def main(args):
    web_object = xbot.web.create("https://www.w3schools.com/tags/tryit.asp?filename=tryhtml5_input_type_file","chrome")
    web_object.find("上传按钮").upload([r'D:\logo.gif'])
```

**执行逻辑：** 用谷歌浏览器打开www.w3schools.com网页 → 找到名称为"上传按钮"的网页元素 → 上传D盘中的logo.gif文件

---

#### `download(file_folder, file_name, wait_complete=True, wait_complete_timeout=300, clipboard_input=True, focus_timeout=1000, dialog_timeout=20)`

自动完成点击下载按钮、在文件保存对话框中输入保存文件信息等系列操作。

**参数：**
- `file_folder`：保存下载文件的文件夹
- `file_name`：自定义保存的文件名，若为空，用下载资源默认文件名
- `wait_complete`：是否等待下载完成，默认为 `True`（等待下载完成）
- `wait_complete_timeout`：等待下载超时时间，单位(秒)，默认为300秒
- `clipboard_input`：文件选择是否用剪切板输入，默认为 `True`（使用剪切板）
- `focus_timeout`：焦点超时时间(获取焦点和输入操作的间隔)，默认1000毫秒
- `dialog_timeout`：点击上传按钮后，等待文件选择框的最大时间，单位（秒）

**返回值：**
- `str`：返回下载文件所在的位置

**示例：**
```python
import xbot
from xbot import print, sleep

def main(args):
    web_object = web.create("www.baidu.com", "chrome")
    web_object.find("百度输入框").input("百度网盘{enter}", contains_hotkey=True)
    download_file_name = web_object.find("立即下载").download("D:\\", "BaiduNetdisk.exe", wait_complete=True, wait_complete_timeout=300)
    print(download_file_name)
```

**执行逻辑：** 用谷歌浏览器打开百度网页 → 找到名称为"百度输入框"的网页元素并输入"百度网盘"，按下回车键 → 找到名称为"立即下载"的网页元素并下载到本地保存 → 打印输出文件下载位置

---

### 表格操作

#### `extract_table()`

获取当前元素所属表格的内容列表。

**参数：**
- 无

**返回值：**
- `List[Tuple]`：返回数据表格内容

**示例1 - 抓取单页：**
```python
from xbot import web

def main(args):
    browser = xbot.web.get_active() 
    rows = browser.extract_table('数据列表')  # rows是二维表格, 如: [['a', 'b'], ['c', 'd']]
```

**示例2 - 抓取多页：**
```python
from xbot import web

def main(args):
    table = []  # table的最终结果是二维表格, 如: [['a', 'b'], ['c', 'd']]
    browser = xbot.web.get_active()
    for i in range(1):
        rows = browser.extract_table('数据列表')
        table.extend(rows)  # 追加一页数据
        if i == 1 - 1:  # 最后一页无需点击下一页
            break
        browser.find('按钮').click()  # 点击下一页
        xbot.sleep(2)  # 等待异步数据加载完成(非必须)
```

**执行逻辑：** 获取当前已打开的网页对象 → 找到名称为"整表数据表格"的网页元素 → 进行整表的批量数据抓取

## 操作类型总结

| 操作类型 | 方法 | 说明 |
|----------|------|------|
| **元素关系** | `parent()` | 获取父元素 |
| | `children()` | 获取所有子元素 |
| | `child_at()` | 获取指定位置子元素 |
| | `previous_sibling()` | 获取上一个兄弟元素 |
| | `next_sibling()` | 获取下一个兄弟元素 |
| **鼠标操作** | `click()` | 单击元素 |
| | `dblclick()` | 双击元素 |
| | `hover()` | 悬停元素 |
| | `drag_to()` | 拖拽元素 |
| **输入操作** | `input()` | 填写输入框 |
| | `clipboard_input()` | 剪切板输入 |
| | `focus()` | 激活元素 |
| **内容获取** | `get_text()` | 获取文本内容 |
| | `get_html()` | 获取HTML内容 |
| | `get_value()` | 获取元素值 |
| | `set_value()` | 设置元素值 |
| **复选框** | `check()` | 设置复选框 |
| | `is_checked()` | 判断是否选中 |
| **下拉框** | `select()` | 单选下拉框 |
| | `select_multiple()` | 多选下拉框 |
| | `select_by_index()` | 按索引选择 |
| | `select_multiple_by_index()` | 按索引多选 |
| | `get_select_options()` | 获取下拉框选项 |
| | `get_all_select_items()` | 获取所有选项 |
| | `get_selected_item()` | 获取选中项 |
| **属性操作** | `set_attribute()` | 设置属性 |
| | `get_attribute()` | 获取属性 |
| | `get_all_attributes()` | 获取所有属性 |
| **状态判断** | `is_enabled()` | 判断是否可用 |
| | `is_displayed()` | 判断是否可见 |
| **截图操作** | `screenshot()` | 截图保存 |
| | `screenshot_to_clipboard()` | 截图到剪切板 |
| **文件操作** | `upload()` | 上传文件 |
| | `download()` | 下载文件 |
| **表格操作** | `extract_table()` | 提取表格数据 |
