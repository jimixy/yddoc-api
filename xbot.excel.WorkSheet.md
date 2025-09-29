# xbot.excel.WorkSheet 模块

## 描述

对工作表对象进行处理，如获取Excel内容、写入Excel内容、清除Excel内容等。

## 类

### `WorkSheet`

Excel工作表类，用于操作Excel工作表的各种功能。

## 方法

### 数据读取

#### `get_cell(row_num, col_name)`

获取工作表中指定单元格的内容。

**参数：**
- `row_num`：指定单元格的行号，行号从1开始
- `col_name`：指定单元格的列名，列名从'A'开始

**返回值：**
- `any`：返回工作表中指定单元格内容

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    data = worksheet.get_cell(10, 'B')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表中第10行第B列单元格的内容

---

#### `get_row(row_num)`

获取工作表中指定行内容。

**参数：**
- `row_num`：指定行号，行号从1开始

**返回值：**
- `List[any]`：返回读取到的内容列表

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    data = worksheet.get_row(1)
    print(data)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表中第一行内容 → 打印获取到的内容

---

#### `get_column(col_name)`

获取工作表中指定列内容。

**参数：**
- `col_name`：指定列名，列名从'A'开始

**返回值：**
- `List[any]`：返回读取到的内容列表，如['a', 'b', 'c', 'd']

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    data = worksheet.get_column('A')
    print(data)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表中第'A'列内容 → 打印获取到的内容

---

#### `get_range(begin_row_num, begin_column_name, end_row_num, end_column_name)`

获取工作表中指定区域的内容。

**参数：**
- `begin_row_num`：起始单元格行号，行号从1开始
- `begin_column_name`：起始单元格列名，列名从A开始
- `end_row_num`：结束单元格行号，行号从1开始
- `end_column_name`：结束单元格列名，列名从A开始

**返回值：**
- `List[Tuple]`：返回读取到的二维列表

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    data = worksheet.get_range(1, 'A', 3, 'F')
    print(data)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表中起始单元格A1到结束单元格F3的矩形区域内容 → 打印获取到的内容

---

### 数据写入

#### `set_cell(row_num, col_name, value)`

在工作表指定单元格写入内容。

**参数：**
- `row_num`：指定单元格的行号
- `col_name`：指定单元格的列名
- `value`：要写入到单元格中的内容

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.set_cell(10, 'B', 'hello world')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 在工作表第10行第B列单元格写入'hello world'

---

#### `set_row(row_num, values, begin_column_name='A')`

设置工作表行内容。

**参数：**
- `row_num`：指定要写入内容的行号，行号从1开始
- `values`：要写入的内容，必须是一个列表类型
- `begin_column_name`：指定写入内容的开始列名，默认值为'A'

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.set_row(1, ['a', 1, 2], begin_column_name='A')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 在第1行，第A列写入：['a', 1, 2]

---

#### `set_column(col_name, values, begin_row_num=1)`

向工作表写入列内容。

**参数：**
- `col_name`：指定要写入内容的列名
- `values`：要写入的内容，必须是一个列表类型
- `begin_row_num`：指定写入内容的开始行号，默认值为1

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.set_column('A', [1,2,3,4,5,6,7,8,9,0], begin_row_num=1)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 从第1行开始设置第A列数据值为[1,2,3,4,5,6,7,8,9,0]

---

#### `set_range(row_num, col_name, values)`

向工作表指定区域写入内容。

**参数：**
- `row_num`：写入区域起始行号，行号从1开始
- `col_name`：写入区域起始列名，列名从A开始
- `values`：要写入的内容，必须是一个二维数组

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.set_range(1, 'A', [['1','2','3'],['a','b','c']])
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 从A1处开始写入内容[['1','2','3'],['a','b','c']]

---

### 行操作

#### `append_row(values, begin_column_name='A')`

在工作表的最后追加一行内容。

**参数：**
- `values`：要写入的值，必须是一个列表类型
- `begin_column_name`：设置开始的单元格列名，默认值为A

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.append_row([1,2,3,4,5,6,7,8,9,0], begin_column_name='B')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 在工作表的最后追加一行内容，起始写入单元格的列名为B，内容为[1,2,3,4,5,6,7,8,9,0]

---

#### `insert_row(row_num, values, begin_column_name='A')`

在工作表中插入一行内容。

**参数：**
- `row_num`：插入位置的行号，行号从1开始
- `values`：要插入的值，必须是一个列表类型
- `begin_column_name`：插入内容的起始列名，默认值为A

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.insert_row(10, [1,2,3,4,5,6,7,8,9,0], begin_column_name='A')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 往工作表第10行插入一条记录，行开始单元格列名为A插入值为[1,2,3,4,5,6,7,8,9,0]

---

#### `remove_row(row_num)`

移除工作表的某一行内容。

**参数：**
- `row_num`：要移除的行号

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.remove_row(10)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 移除工作表中第10行的数据

---

### 列操作

#### `remove_column(column_name)`

移除工作表的某一列内容。

**参数：**
- `column_name`：要移除的列名

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.remove_column('D')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 移除工作表中第D列的数据

---

#### `insert_column(column_name, values, begin_row_index=1)`

插入列。

**参数：**
- `column_name`：插入数据的起始列名
- `values`：插入数据
- `begin_row_index`：开始插入的行号

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.insert_column('D', [1, 'a', 2], 3)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 从第3行开始，将列表[1, 'a', 2]插入到D列

---

### 内容管理

#### `clear()`

清空工作表内容。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.clear()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 清空工作表内容

---

#### `clear_range(begin_row_num, begin_column_name, end_row_num, end_column_name)`

清空指定的区域内容。

**参数：**
- `begin_row_num`：起始单元格行号，行号从1开始
- `begin_column_name`：起始单元格列名，列名从A开始
- `end_row_num`：结束单元格行号，行号从1开始
- `end_column_name`：结束单元格列名，列名从A开始

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.clear_range(1, 'A', 3, 'C')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 清空工作表中从单元格A1到单元格C3的矩形内容区域

---

### 信息获取

#### `get_row_count()`

获取工作表的总行数。

**参数：**
- 无

**返回值：**
- `int`：返回工作表的总行数

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    count = worksheet.get_row_count()
    print(count)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表当前数据的总行数 → 打印总行数

---

#### `get_column_count()`

获取工作表的总列数。

**参数：**
- 无

**返回值：**
- `int`：返回工作表的总列数

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    count = worksheet.get_column_count()
    print(count)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表当前数据的总列数 → 打印总列数

---

#### `get_name()`

获取工作表的名称。

**参数：**
- 无

**返回值：**
- `str`：返回工作表的名称

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    name = worksheet.get_name()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作表当前数据的名称

---

### 区域操作

#### `select_range(begin_row_num, begin_column_name, end_row_num, end_column_name)`

选中工作表的指定内容区域。

**参数：**
- `begin_row_num`：起始单元格行号，行号从1开始
- `begin_column_name`：起始单元格列名，列名从A开始
- `end_row_num`：结束单元格行号，行号从1开始
- `end_column_name`：结束单元格列名，列名从A开始

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.select_range(1, 'A', 3, 'C')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 选中工作表中从单元格A1到单元格C3的矩形内容区域

---

#### `copy_range(begin_row_num, begin_column_name, end_row_num, end_column_name)`

拷贝指定的区域内容到剪切板。

**参数：**
- `begin_row_num`：起始单元格行号，行号从1开始
- `begin_column_name`：起始单元格列名，列名从A开始
- `end_row_num`：结束单元格行号，行号从1开始
- `end_column_name`：结束单元格列名，列名从A开始

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.copy_range(1, 'A', 3, 'C')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 拷贝工作表中从单元格A1到单元格C3的矩形内容区域

---

#### `paste_range(row_num, column_name)`

从指定的起始单元格粘贴剪切板数据（该接口已弃用，后续不再维护，建议使用接口paste_range_ex）。

**参数：**
- `row_num`：起始单元格行号，行号从1开始
- `column_name`：起始单元格列名，列名从A开始

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.paste_range(3, 'C')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 从指定的起始单元格C3粘贴剪切板数据

---

#### `paste_range_ex(row_num, column_name, paste_type, paste_special_operation, skip_blanks, transpose)`

从指定的起始单元格粘贴剪切板数据，扩展选择性粘贴功能。

**参数：**
- `row_num`：起始单元格行号，行号从1开始
- `column_name`：起始单元格列名，列名从A开始
- `paste_type`：粘贴类型，类型参数代码如下：

| 粘贴类型 | 参数代码 |
|----------|----------|
| 全部 | -4104 |
| 公式 | -4123 |
| 数值 | -4163 |
| 格式 | -4122 |
| 批注 | -4144 |
| 有效性验证 | 6 |
| 所有使用源主题的单元 | 13 |
| 边框除外 | 7 |
| 列宽 | 8 |
| 公式和数字格式 | 11 |
| 值和数字格式 | 12 |

- `paste_special_operation`：粘贴运算，参数代码如下：

| 粘贴类型 | 参数代码 |
|----------|----------|
| 无 | -4142 |
| 加 | 2 |
| 减 | 3 |
| 乘 | 4 |
| 除 | 5 |

- `skip_blanks`：是否跳过空单元，默认为False（不跳过）
- `transpose`：是否选择转置，默认为False（不转置）

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    worksheet.paste_range_ex(3, 'C', -4104, -4142, False, False)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 从指定的起始单元格C3粘贴剪切板数据，粘贴类型为全部

---

### 位置查找

#### `get_first_free_column()`

获取第一个可用列。

**参数：**
- 无

**返回值：**
- `str`：返回工作表的列名

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    column = worksheet.get_first_free_column()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取当前列表的第一个可用列

---

#### `get_first_free_column_on_row(row_num)`

获取行的第一个可用列。

**参数：**
- `row_num`：行号

**返回值：**
- `str`：返回工作表的列名

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    column = worksheet.get_first_free_column_on_row(3)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取当前列表的第3行上的第一个可用列

---

#### `get_first_free_row()`

获取第一个可用行。

**参数：**
- 无

**返回值：**
- `int`：返回工作表的行号

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    row = worksheet.get_first_free_row()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取当前列表的第一个可用行

---

#### `get_first_free_row_on_column(column_name)`

获取列的第一个可用行。

**参数：**
- `column_name`：列名

**返回值：**
- `int`：返回工作表的行号

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    row = worksheet.get_first_free_row_on_column('D')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取当前列表的D列上的第一个可用行

---

### 显示控制

#### `set_row_hidden(row_num, hidden=False)`

设置行隐藏属性。

**参数：**
- `row_num`：行号，list，行号从1开始
- `hidden`：隐藏属性，默认为False（取消隐藏）

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    row_list = [1,2,3]
    worksheet.set_row_hidden(row_list, True)
    workbook.save()
    workbook.close()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 设置第1行到第3行隐藏

---

#### `set_column_hidden(column_name, hidden=False)`

设置列隐藏属性。

**参数：**
- `column_name`：列名列表，列名从A开始
- `hidden`：隐藏属性，默认为False（取消隐藏）

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
    col_list = ['A','B','C']
    worksheet.set_column_hidden(col_list, True)
    workbook.save()
    workbook.close()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 设置第A列到第C列隐藏 → 保存Excel表 → 关闭Excel表

## 功能分类总结

| 功能类别 | 方法 | 说明 |
|----------|------|------|
| **数据读取** | `get_cell()` | 获取指定单元格内容 |
| | `get_row()` | 获取指定行内容 |
| | `get_column()` | 获取指定列内容 |
| | `get_range()` | 获取指定区域内容 |
| **数据写入** | `set_cell()` | 写入单元格内容 |
| | `set_row()` | 写入行内容 |
| | `set_column()` | 写入列内容 |
| | `set_range()` | 写入区域内容 |
| **行操作** | `append_row()` | 追加行内容 |
| | `insert_row()` | 插入行内容 |
| | `remove_row()` | 移除行内容 |
| **列操作** | `remove_column()` | 移除列内容 |
| | `insert_column()` | 插入列内容 |
| **内容管理** | `clear()` | 清空工作表内容 |
| | `clear_range()` | 清空指定区域内容 |
| **信息获取** | `get_row_count()` | 获取总行数 |
| | `get_column_count()` | 获取总列数 |
| | `get_name()` | 获取工作表名称 |
| **区域操作** | `select_range()` | 选中指定区域 |
| | `copy_range()` | 复制区域到剪切板 |
| | `paste_range()` | 粘贴剪切板内容（已弃用） |
| | `paste_range_ex()` | 扩展粘贴功能 |
| **位置查找** | `get_first_free_column()` | 获取第一个可用列 |
| | `get_first_free_column_on_row()` | 获取行的第一个可用列 |
| | `get_first_free_row()` | 获取第一个可用行 |
| | `get_first_free_row_on_column()` | 获取列的第一个可用行 |
| **显示控制** | `set_row_hidden()` | 设置行隐藏属性 |
| | `set_column_hidden()` | 设置列隐藏属性 |

## 注意事项

1. **索引从1开始**：所有行号都从1开始计数，不是从0开始
2. **列名格式**：列名使用字母格式，从'A'开始
3. **数据类型**：写入数据时，`values`参数必须是列表类型
4. **区域操作**：区域操作需要指定起始和结束位置
5. **剪切板操作**：复制和粘贴操作会使用系统剪切板
6. **隐藏属性**：设置隐藏属性后需要保存工作簿才能生效
7. **已弃用接口**：`paste_range()`接口已弃用，建议使用`paste_range_ex()`
8. **数据格式**：二维数组写入时，确保数据格式正确
9. **文件操作**：操作完成后建议保存工作簿
10. **错误处理**：确保指定的行号和列名在有效范围内
