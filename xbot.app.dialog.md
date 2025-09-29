# xbot.app.dialog 模块

## 描述

调取各类对话框，实现与影刀机器人的交互。如消息对话框、自定义对话框。

## 方法

### `show_alert(message, title='提示')`

打开消息对话框。

**参数：**
- `message`：需要在消息对话框中展示的内容
- `title`：消息对话框标题，若不填，默认为"提示"

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.dialog.show_alert('hello world', '提示')
```

**执行逻辑：** 调开消息对话框，对话框标题设置为"提示"，对话框内容为"hello world"

---

### `show_confirm(message, title='请确认')`

打开确认对话框。

**参数：**
- `message`：需要在确认对话框中展示的内容
- `title`：确认对话框标题，默认标题内容为"请确认"

**返回值：**
- `bool`：返回确认对话框选择结果，选择确认返回 True，否则返回 False

**示例：**
```python
from xbot import app

def main(args):
    is_confirm = app.dialog.show_confirm('hello world')
    print(is_confirm)
```

**执行逻辑：** 调开确认对话框，对话框内容为"hello world" → 打印输出与对话框交互的结果

---

### `show_custom_dialog(settings)`

打开自定义对话框。

**参数：**
- `settings`：自定义对话框配置 JSON 串，包含对话框标题和自定义控件配置

**JSON 结构：**
```json
{
    "dialog_title": "标题",
    "default_btn": "确定",
    "use_wait_timeout": true,
    "timeout": 10,
    "settings": {
        "editors": [
            {"type": "CheckBox", "label": "复选框"},
            ...
        ]
    }
}
```

**配置参数说明：**

| 参数 | 说明 |
|------|------|
| `dialog_title` | 对话框标题，可为空 |
| `default_btn` | 当对话框出现时间超时时，指定点击默认按钮 |
| `use_wait_timeout` | 是否启用超时自动点击 |
| `timeout` | 超时时间。0=不等待，-1=一直等待，>0=等待指定秒数 |
| `editors` | 自定义控件列表，每个控件为一个字典 |

**支持的控件类型：**

| 控件类型 | 说明 |
|----------|------|
| `TextBox` | 输入框 |
| `Number` | 数字框 |
| `Password` | 密码框 |
| `TextArea` | 文本域（多行文本） |
| `Label` | 文本标签 |
| `CheckBox` | 复选框 |
| `Select` | 下拉框 |
| `MultiSelect` | 多选下拉框 |
| `Date` | 日期控件 |
| `File` | 文件选择器 |
| `List` | 列表 |
| `MultiList` | 多选列表 |
| `DataGrid` | 数据表格 |

**控件参数：**

| 参数 | 说明 |
|------|------|
| `type` | 自定义控件类型 |
| `label` | 自定义控件标题 |
| `nullText` | 空白提示信息，主要用于输入类控件 |
| `value` | 程序运行时控件中的默认值 |

**特殊控件参数：**

- **下拉框控件**：`options` - 选项列表，包含 `display`（显示文本）和 `value`（值）
- **文件选择器**：`kind` - 文件选择器种类（OpenFile/SaveFile/SelectFolder）

**返回值：**
- `object_dict`：返回自定义对话框处理结果，类型为字典

**示例1 - 输入框：**
```python
from xbot import app

def main(args):
    value = app.dialog.show_custom_dialog({
        "dialog_title": "hello", 
        "default": "确定",
        "use_wait_timeout": True,
        "timeout": 10,
        "settings": {
            "editors": [{
                "type": "TextBox", 
                "label": "输入框", 
                "nullText": None, 
                "value": "hello world"
            }]
        }
    })
    print(value)
```

**示例2 - 复选框：**
```python
from xbot import app

def main(args):
    value = app.dialog.show_custom_dialog({
        "dialog_title": "hello",
        "settings": {
            "editors": [{
                "type": "CheckBox",
                "label": "复选框",
                "value": True
            }]
        }
    })
    print(value)
```

**示例3 - 下拉框：**
```python
from xbot import app

def main(args):
    value = app.dialog.show_custom_dialog({
        "dialog_title": "hello",
        "settings": {
            "editors": [{
                "type": "Select",
                "label": "下拉选择框",
                "value": "2",
                "options": [
                    {"display": "选项1", "value": "1"},
                    {"display": "选项2", "value": "2"}
                ]
            }]
        }
    })
    print(value)
```

**示例4 - 多种控件：**
```python
from xbot import app

def main(args):
    value = app.dialog.show_custom_dialog({
        "dialog_title": "hello",
        "settings": {
            "editors": [
                {
                    "type": "Password",
                    "label": "密码框",
                    "nullText": None,
                    "value": "123"
                },
                {
                    "type": "TextArea",
                    "label": "文本域",
                    "nullText": "hello world",
                    "value": None
                },
                {
                    "type": "Date",
                    "label": "时间",
                    "value": "2020/04/18"
                },
                {
                    "type": "File",
                    "label": "文件选择器",
                    "nullText": "请选择文件",
                    "kind": "OpenFile"
                }
            ]
        }
    })
    print(value)
```

---

### `show_message_box(title, message, button='ok', *, timeout=-1, default_button=None)`

打开消息对话框。

**参数：**
- `title`：消息对话框标题
- `message`：消息对话框要展示的信息
- `button`：消息对话框中的按钮组合
  - `'ok'`：确定
  - `'okcancel'`：确定/取消
  - `'yesno'`：是/否
  - `'yesnocancel'`：是/否/取消
- `timeout`：对话框等待点击超时时间，默认一直等待
  - `-1`：一直等待
  - `0`：不等待
  - `>0`：等待指定秒数
- `default_button`：超时时默认点击的按钮，仅在超时时间大于0时起效

**返回值：**
- `str`：返回消息对话框交互结果，如："ok" 或 "cancel" 等

**示例：**
```python
from xbot import app

def main(args):
    button_result = app.dialog.show_message_box(
        '提示',
        '您开启了消息对话框',
        'okcancel', 
        timeout=10, 
        default_button='cancel'
    )
    print(button_result)
```

**执行逻辑：** 打开消息对话框，设置标题为"提示"，内容为"您开启了消息对话框"，按钮为"确定/取消"，10秒后若没有交互则默认点击取消

---

### `show_workbook_dialog(title, message)`

打开数据表格对话框。

**参数：**
- `title`：数据表格对话框标题
- `message`：数据表格对话框提示信息

**返回值：**
- `str`：返回数据表格对话框处理结果，如："ok" 或 "cancel" 等

**示例：**
```python
from xbot import app

def main(args):
    result = app.dialog.show_workbook_dialog('数据表格', '请在数据表格中放入数据')
    print(result)
```

**执行逻辑：** 打开标题为"数据表格"，提示信息为"请在数据表格中放入数据"的数据表格对话框

---

### `show_notification(message, placement='rightbottom', level='info', timeout=3)`

打开消息通知框。

**参数：**
- `message`：消息通知框的通知内容
- `placement`：通知消息在屏幕上的显示位置
  - `'top'`：屏幕顶部
  - `'bottom'`：屏幕底部
  - `'rightbottom'`：屏幕右下角（默认）
- `level`：通知消息的消息级别
  - `'info'`：信息级别（默认）
  - `'warning'`：警告
  - `'error'`：错误
- `timeout`：通知消息框显示时长，默认3秒

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.dialog.show_notification('hello', placement='top', level='info')
```

**执行逻辑：** 在屏幕上方展示通知消息框，内容为"hello"，通知类型为信息级别，持续时间为3秒
