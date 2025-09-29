# xbot.excel 模块

## 描述

对Excel对象进行操作，如创建Excel对象、打开Excel文件等。

## 方法

### `create(kind='office', visible=True)`

创建并返回Excel对象。

**参数：**
- `kind`：创建方式，有四种方式：
  - `'office'`：使用 Microsoft Office
  - `'wps'`：使用 WPS
  - `'openpyxl'`：使用 Openpyxl
  - `'auto_check'`：自动检查，优先使用 office 创建
  - 若 office 和 wps 都不存在，则抛出 ValueError 异常
- `visible`：用于控制自动化操作是否用户级可见，并不限制自动化的能力，仅在office和wps下有效

**返回值：**
- `WorkBook`：返回创建的Excel对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.create(kind='office', visible=True)
```

**执行逻辑：** 使用 Microsoft Office 创建Excel对象

---

### `open(file_name, kind='office', visible=True)`

打开Excel文件并返回Excel对象。

**参数：**
- `file_name`：Excel文件路径
- `kind`：打开方式，有四种方式：
  - `'office'`：使用 Microsoft Office
  - `'wps'`：使用 WPS
  - `'openpyxl'`：使用 Openpyxl
  - `'auto_check'`：自动检查，优先使用 office 打开
  - 若 office 和 wps 都不存在，则抛出 ValueError 异常
- `visible`：用于控制自动化操作是否用户级可见，并不限制自动化的能力，仅在office和wps下有效

**返回值：**
- `WorkBook`：返回打开的Excel对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
```

**执行逻辑：** 使用 Microsoft Office 打开Excel文件："D:\test.xlsx"

---

### `get_active_workbook(kind)`

获取当前激活的Excel。

**参数：**
- `kind`：打开方式，有四种方式：
  - `'office'`：使用 Microsoft Office
  - `'wps'`：使用 WPS
  - `'openpyxl'`：使用 Openpyxl
  - `'auto_check'`：自动检查，优先使用 office 打开
  - 若 office 和 wps 都不存在，则抛出 ValueError 异常

**返回值：**
- `WorkBook`：返回当前激活的Excel对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.get_active_workbook(kind='auto_check')
```

**执行逻辑：** 获取当前激活的Excel

## 功能分类总结

| 功能类别 | 方法 | 说明 |
|----------|------|------|
| **Excel对象创建** | `create()` | 创建新的Excel对象 |
| **Excel文件操作** | `open()` | 打开现有Excel文件 |
| **Excel对象获取** | `get_active_workbook()` | 获取当前激活的Excel对象 |

## 支持的Excel类型

| 类型 | 说明 | 特点 |
|------|------|------|
| `'office'` | Microsoft Office | 功能最全面，支持所有操作 |
| `'wps'` | WPS Office | 兼容Office，功能较全面 |
| `'openpyxl'` | Openpyxl库 | 纯Python实现，无需安装Office |
| `'auto_check'` | 自动检测 | 优先使用Office，其次WPS |
