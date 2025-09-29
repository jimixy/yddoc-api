# xbot.app.databook 模块

## 描述

对影刀内置的数据表格进行操作（如获取行内容、数据表格内写入行内容等）。

## 方法

### `get_row(row_num)`

获取数据表格指定行内容。

**参数：**
- `row_num`：指定行号，行号从1开始

**返回值：**
- `List[str]`：返回读取到的内容列表，如 `['a', 'b', 'c', 'd']`

**示例：**
```python
from xbot import app

def main(args):
    list_value = app.databook.get_row(1)
    print(list_value)
```

**执行逻辑：** 读取数据表格第一行的内容 → 打印获取结果

---

### `set_row(row_num, values, begin_column_name='A')`

向数据表格指定列写入行内容。

**参数：**
- `row_num`：要设置的数据表格行号，行号从1开始
- `values`：要设置的值，必须是一个字符列表类型，如 `['a', 'b', 'c']`
- `begin_column_name`：要写入数据的起始列名，若不填，则默认值为"A"

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.set_row(1, ['hello world'], begin_column_name='A')
```

**执行逻辑：** 在数据表格第1行A列写入"hello world"

---

### `append_row(values, begin_column_name='A')`

在数据表格追加一行内容。

**参数：**
- `values`：要设置的值，必须是一个列表类型
- `begin_column_name`：设置开始的单元格列名，若不填，默认值为"A"

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.append_row([1,2,3,4,5,6,7,8,9,0], begin_column_name='B')
```

**执行逻辑：** 在数据表格的最后追加一行内容，起始写入单元格的列名为B，内容为[1,2,3,4,5,6,7,8,9,0]

---

### `insert_row(row_num, values, begin_column_name='A')`

往数据表格中插入一行内容。

**参数：**
- `row_num`：插入位置的行号，行号从1开始
- `values`：要设置的值，必须是一个列表类型
- `begin_column_name`：起始开始的单元格列名，若不填，默认值为"A"

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.insert_row(10, [0,1,2,3,4,5,6,7,8,9], begin_column_name='A')
```

**执行逻辑：** 在数据表格第10行写入'0-9'十个数字，起始列为A

---

### `remove_row(row_num)`

删除数据表格指定行内容。

**参数：**
- `row_num`：要移除的行号

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.remove_row(2)
```

**执行逻辑：** 删除数据表格第二行的内容

---

### `get_cell(row_num, col_name)`

获取数据表格指定单元格内容。

**参数：**
- `row_num`：指定单元格的行号
- `col_name`：指定单元格的列名

**返回值：**
- `str`：数据表格指定单元格内容

**示例：**
```python
from xbot import app

def main(args):
    value = app.databook.get_cell(2, 'B')
    print(value)
```

**执行逻辑：** 获取数据表格第2行B列单元格的内容 → 输出获取结果

---

### `set_cell(row_num, col_name, value)`

在数据表格指定单元格写入内容。

**参数：**
- `row_num`：单元格行号
- `col_name`：单元格列名
- `value`：要写入到单元格中的内容

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.set_cell(1, 'A', 'hello')
```

**执行逻辑：** 在数据表格第1行A列写入字符串'hello'

---

### `set_column(col_name, values, begin_row_num=1)`

在数据表格指定列中写入内容。

**参数：**
- `col_name`：列名，指要写入内容的列位置
- `values`：写入的值，必须是一个列表类型
- `begin_row_num`：写入列内容的起始行号，若不填，默认行号为1

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.set_column('A', [0,1,2,3,4,5,6,7,8,9], begin_row_num=1)
```

**执行逻辑：** 在数据表格A列第1行开始写入"0-9"十个数字

---

### `clear()`

清空数据表格内容。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.clear()
```

**执行逻辑：** 清空数据表格内容

---

### `get_row_count()`

获取数据表格的总行数（这里指的是已写入数据的总行数）。

**参数：**
- 无

**返回值：**
- `int`：数据表格的总行数

**示例：**
```python
from xbot import app

def main(args):
    count = app.databook.get_row_count()
    print(count)
```

**执行逻辑：** 获取数据表格当前数据的总行数 → 打印输出数据表格总行数

---

### `get_range(area_begin_row_num, area_begin_column_name, area_end_row_num, area_end_column_name)`

获取数据表格指定区域的内容。

**参数：**
- `area_begin_row_num`：起始单元格行号，行号从1开始
- `area_begin_column_name`：起始单元格列名，列名从A开始
- `area_end_row_num`：结束单元格行号，行号从1开始
- `area_end_column_name`：结束单元格列名，列名从A开始

**返回值：**
- `List[Tuple]`：指定区域的数据，类型为二维列表

**示例：**
```python
from xbot import app

def main(args):
    list_value = app.databook.get_range(1, 'A', 3, 'F')
    print(list_value)
```

**执行逻辑：** 获取数据表格A1单元格到F3单元格中的内容 → 打印输出指定区域内容

---

### `set_range(row_num, col_name, values)`

向数据表格指定区域写入内容。

**参数：**
- `row_num`：写入区域内容的起始行号，行号从1开始
- `col_name`：写入区域内容的起始列名，列名从A开始
- `values`：要设置的内容，必须是一个二维数组

**返回值：**
- 无

**示例：**
```python
from xbot import app

def main(args):
    app.databook.set_range(1, 'A', [['1','2','3'],['a','b','c']])
```

**执行逻辑：** 在第1行第A列写入 `[['1','2','3'],['a','b','c']]`

## 操作类型总结

| 操作类型 | 方法 | 说明 |
|----------|------|------|
| **行操作** | `get_row()` | 获取指定行内容 |
| | `set_row()` | 设置指定行内容 |
| | `append_row()` | 追加新行 |
| | `insert_row()` | 插入新行 |
| | `remove_row()` | 删除指定行 |
| **单元格操作** | `get_cell()` | 获取单元格内容 |
| | `set_cell()` | 设置单元格内容 |
| **列操作** | `set_column()` | 设置整列内容 |
| **区域操作** | `get_range()` | 获取区域内容 |
| | `set_range()` | 设置区域内容 |
| **表格操作** | `clear()` | 清空表格 |
| | `get_row_count()` | 获取总行数 |
