# xbot.excel.WorkBook 模块

## 描述

对工作簿进行各种处理，如获取Sheet页、激活Sheet页、创建Sheet页、保存为Excel文件、另存为Excel文件、执行宏、关闭工作簿等。

## 类

### `WorkBook`

Excel工作簿类，用于操作Excel工作簿的各种功能。

## 方法

### Sheet页操作

#### `get_active_sheet()`

获取工作簿中激活的Sheet页。

**参数：**
- 无

**返回值：**
- `WorkSheet`：Sheet页对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_active_sheet()
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取当前激活的Sheet页

---

#### `get_sheet_by_index(index)`

获取工作簿中指定位置的Sheet页。

**参数：**
- `index`：目标Sheet页在工作簿中的索引位置，从1开始计数

**返回值：**
- `WorkSheet`：Sheet页对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_sheet_by_index(1)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作簿中第一个Sheet页

---

#### `get_sheet_by_name(name)`

获取工作簿中指定名称的Sheet页。

**参数：**
- `name`：目标Sheet页的名称

**返回值：**
- `WorkSheet`：Sheet页对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.get_sheet_by_name('Sheet1')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 获取工作簿中指定名称的Sheet页

---

#### `get_all_sheets()`

获取所有的Sheet页。

**参数：**
- 无

**返回值：**
- `List[WorkSheet]`：Sheet页对象列表

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    sheets = workbook.get_all_sheets()
```

**执行逻辑：** 获取Excel文件 "D:\test.xlsx" 所有Sheet页对象

---

### Sheet页激活

#### `active_sheet_by_index(index)`

激活工作簿中指定位置的Sheet页。

**参数：**
- `index`：目标Sheet页在工作簿中的索引位置，从1开始计数

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.active_sheet_by_index(1)
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 激活第一个Sheet页

---

#### `active_sheet_by_name(name)`

激活工作簿中指定名称的Sheet页。

**参数：**
- `name`：目标Sheet页的名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.active_sheet_by_name('Sheet1')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 激活名称为 'Sheet1' 的Sheet页

---

### Sheet页创建和管理

#### `create_sheet(name, create_way)`

在工作簿中创建新的Sheet页。

**参数：**
- `name`：Sheet页名称
- `create_way`：添加方式，可选择两种添加方式：
  - `'first'`：作为第一个Sheet页
  - `'last'`：作为最后一个Sheet页

**返回值：**
- `WorkSheet`：Sheet页对象

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    worksheet = workbook.create_sheet('SheetTest', 'last')
```

**执行逻辑：** 可视化打开Excel工作表 "D:\test.xlsx" → 追加一个名称为 'SheetTest' 的Sheet页

---

#### `delete_sheet(name)`

删除Sheet页。

**参数：**
- `name`：Sheet页名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.delete_sheet('Sheet1')
```

**执行逻辑：** 删除Excel文件 "D:\test.xlsx" 的Sheet1页

---

#### `rename_sheet(name, new_name)`

重命名Sheet页。

**参数：**
- `name`：待修改的Sheet页名称
- `new_name`：修改后的Sheet页名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.rename_sheet('Sheet1', '测试页面1')
```

**执行逻辑：** 可视化打开Excel文件 "D:\test.xlsx" → 修改Sheet1页名称为'测试页面1'

---

### Sheet页复制

#### `copy_sheet(name, new_name)`

拷贝Sheet页。

**参数：**
- `name`：待拷贝的Sheet页名称
- `new_name`：新的Sheet页名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.copy_sheet('Sheet1', 'Sheet2')
```

**执行逻辑：** 拷贝Excel文件 "D:\test.xlsx" 的Sheet1页到新的Sheet2页

---

#### `copy_sheet_to_workbook(name, workbook, new_name)`

拷贝Sheet页到指定Workbook。

**参数：**
- `name`：待拷贝的Sheet页名称
- `workbook`：目标Workbook名称
- `new_name`：新的Sheet页名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook1 = excel.open('D:\\test1.xlsx', kind='office', visible=True)
    workbook.copy_sheet_to_workbook('Sheet1', workbook1, 'Sheet2')
```

**执行逻辑：** 可视化打开Excel文件 "D:\test.xlsx" "D:\test1.xlsx" → 将文件 "D:\test.xlsx" 的Sheet1页拷贝到Excel文件 "D:\test1.xlsx" 的Sheet2页

---

### 文件操作

#### `save()`

将工作簿保存为Excel文件。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.save()
```

**执行逻辑：** 打开Excel文件 "D:\test.xlsx" 后保存

---

#### `save_as(filename)`

将工作簿另存为Excel文件。

**参数：**
- `filename`：另存为路径

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.save_as('D:\\test1.xlsx')
```

**执行逻辑：** 打开Excel文件 "D:\test.xlsx" 后，另存为'D:\test1.xlsx'

---

#### `close()`

关闭工作簿。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.close()
```

**执行逻辑：** 打开Excel文件 "D:\test.xlsx" 后关闭

---

### 宏操作

#### `execute_macro(macro)`

执行宏。

**参数：**
- `macro`：宏名称

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.execute_macro('macro1')
```

**执行逻辑：** 打开Excel文件 "D:\test.xlsx" 后执行名称为'macro1'的宏

---

### 数据操作

#### `refresh_data()`

刷新数据。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.refresh_data()
```

**执行逻辑：** 可视化打开Excel文件 "D:\test.xlsx" → 刷新文件数据

---

#### `get_selected_range()`

获取当前页的选中区域。

**参数：**
- 无

**返回值：**
- `Tuple`：返回元组类型值——(起始单元格行号, 起始单元格列名, 终止单元格行号, 终止单元格列名)

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    range_info = workbook.get_selected_range()
```

**执行逻辑：** 可视化打开Excel文件 "D:\test.xlsx" → 获取当前页的选中区域

---

### 数据透视表操作

#### `create_pivot_table(setting, source)`

创建数据透视表。

**参数：**
- `setting`：数据透视表配置。setting的JSON串应使用影刀Excel拾取工具从Excel文件中拾取数据透视表数据之后获得
- `source`：数据透视表数据来源

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    
    pivot_setting = '{"sourceType":1,"sheetName":"Sheet6","tableRange":"A1:B7","name":"数据透视表8","properties":[{"name":"ColumnGrand","value":true},{"name":"RowGrand","value":true},{"name":"SubtotalHiddenPageItems","value":false},{"name":"InGridDropZones","value":false},{"name":"LayoutRowDefault","value":2},{"name":"DisplayFieldCaptions","value":true},{"name":"ShowDrillIndicators","value":true},{"name":"DisplayContextTooltips","value":true},{"name":"SortUsingCustomLists","value":true},{"name":"DisplayImmediateItems","value":false},{"name":"FieldListSortAscending","value":false},{"name":"ShowValuesRow","value":false}],"fields":[{"name":"职称","index":"1","formula":null,"customName":"职称","subtotals":[true,false,false,false,false,false,false,false,false,false,false,false],"props":[{"name":"Orientation","value":3},{"name":"ShowAllItems","value":false},{"name":"EnableMultiplePageItems","value":false}]},{"name":"姓名","index":"1","formula":null,"customName":"姓名","subtotals":[true,false,false,false,false,false,false,false,false,false,false,false],"props":[{"name":"Orientation","value":1},{"name":"ShowAllItems","value":false},{"name":"EnableItemSelection","value":true}]},{"name":"工号","index":"1","formula":"","customName":"求和项:工号","subtotals":[true,false,false,false,false,false,false,false,false,false,false,false],"props":[{"name":"Orientation","value":4},{"name":"ShowAllItems","value":false},{"name":"Calculation","value":-4143},{"name":"Function","value":-4157},{"name":"NumberFormat","value":"General"}]}]}'
    
    workbook.create_pivot_table(pivot_setting, 'Sheet1!$C$1:$E$4')
```

**执行逻辑：** 在Excel文件 "D:\test.xlsx" 中创建数据透视表，数据来源为 'Sheet1!1:4'

---

#### `refresh_pivot_table(name_or_index, sheet_name=None)`

刷新数据透视表。

**参数：**
- `name_or_index`：数据透视表名称或位置（从1开始）
- `sheet_name`：透视表所在Sheet页名称，默认为当前激活的Sheet页

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.refresh_pivot_table('1')
```

**执行逻辑：** 在Excel文件 "D:\test.xlsx" 中刷新数据透视表

---

#### `filter_pivot_table(sheet_name, name_or_index, field_name, select_type, filter_value_list)`

筛选数据透视表。

**参数：**
- `sheet_name`：透视表所在Sheet页名称，默认为当前激活的Sheet页
- `name_or_index`：数据透视表名称或位置（从1开始）
- `field_name`：透视表筛选器字段名称
- `select_type`：选择方式，包括'all'、'none'和'partial'
- `filter_value_list`：透视表筛选器选择项内容

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.filter_pivot_table('Sheet1', '1', '职务', 'partial', ['经理', '文员'])
```

**执行逻辑：** 在Excel文件 "D:\test.xlsx" 中筛选数据透视表，筛选职务为经理和文员

---

### 导出操作

#### `export_to_pdf(pdf_name, sheet_name=None, all_sheets=False, override=True)`

导出PDF文件。

**参数：**
- `pdf_name`：PDF文件路径
- `sheet_name`：要导出的Sheet页，默认为当前激活的Sheet名称
- `all_sheets`：是否导出全部Sheet页，默认为False（不全部导出）
- `override`：若导出的PDF文件已存在，是否选择覆盖，默认为True（覆盖）

**返回值：**
- 无

**示例：**
```python
from xbot import excel

def main(args):
    workbook = excel.open('D:\\test.xlsx', kind='office', visible=True)
    workbook.export_to_pdf('D:\\test.pdf', 'Sheet1')
```

**执行逻辑：** 可视化打开Excel文件 "D:\test.xlsx" → 将Sheet1页导出到'D:\test.pdf'

## 功能分类总结

| 功能类别 | 方法 | 说明 |
|----------|------|------|
| **Sheet页操作** | `get_active_sheet()` | 获取激活的Sheet页 |
| | `get_sheet_by_index()` | 按索引获取Sheet页 |
| | `get_sheet_by_name()` | 按名称获取Sheet页 |
| | `get_all_sheets()` | 获取所有Sheet页 |
| **Sheet页激活** | `active_sheet_by_index()` | 按索引激活Sheet页 |
| | `active_sheet_by_name()` | 按名称激活Sheet页 |
| **Sheet页创建和管理** | `create_sheet()` | 创建新Sheet页 |
| | `delete_sheet()` | 删除Sheet页 |
| | `rename_sheet()` | 重命名Sheet页 |
| **Sheet页复制** | `copy_sheet()` | 复制Sheet页 |
| | `copy_sheet_to_workbook()` | 复制Sheet页到其他工作簿 |
| **文件操作** | `save()` | 保存工作簿 |
| | `save_as()` | 另存为工作簿 |
| | `close()` | 关闭工作簿 |
| **宏操作** | `execute_macro()` | 执行宏 |
| **数据操作** | `refresh_data()` | 刷新数据 |
| | `get_selected_range()` | 获取选中区域 |
| **数据透视表操作** | `create_pivot_table()` | 创建数据透视表 |
| | `refresh_pivot_table()` | 刷新数据透视表 |
| | `filter_pivot_table()` | 筛选数据透视表 |
| **导出操作** | `export_to_pdf()` | 导出为PDF |

## 注意事项

1. **索引从1开始**：所有Sheet页索引都从1开始计数，不是从0开始
2. **文件路径**：确保文件路径正确且文件存在，使用双反斜杠或原始字符串
3. **宏执行**：执行宏需要确保宏存在于工作簿中且宏名称正确
4. **数据透视表**：创建数据透视表需要正确的JSON配置，建议使用影刀Excel拾取工具获取
5. **Sheet页操作**：删除或重命名Sheet页前，确保目标Sheet页存在
6. **复制操作**：复制Sheet页到其他工作簿时，目标工作簿必须已打开
7. **PDF导出**：导出PDF时，确保有足够的磁盘空间和写入权限
8. **数据刷新**：刷新数据操作可能需要等待，特别是对于大量数据
