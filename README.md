# 影刀API文档

本目录包含了影刀RPA平台的各个模块API文档，涵盖了数据操作、Excel处理、网页自动化、日志记录等核心功能。

## 📁 模块概览

### 核心模块

| 模块 | 文件 | 功能描述 |
|------|------|----------|
| **Package** | `package.md` | 元素选择器、图像选择器和资源文件操作 |
| **ADO** | `xbot.ado.md` | 数据库连接、SQL执行和数据操作 |
| **Logging** | `xbot.logging.md` | 日志记录（调试、信息、警告、错误） |

### 应用模块

| 模块 | 文件 | 功能描述 |
|------|------|----------|
| **DataBook** | `xbot.app.databook.md` | 影刀内置数据表格操作 |
| **Dialog** | `xbot.app.dialog.md` | 各类对话框交互（消息、确认、自定义等） |

### Excel模块

| 模块 | 文件 | 功能描述 |
|------|------|----------|
| **Excel** | `xbot.excel.md` | Excel对象创建、打开和获取 |
| **WorkBook** | `xbot.excel.WorkBook.md` | 工作簿操作（Sheet管理、文件操作、宏执行等） |
| **WorkSheet** | `xbot.excel.WorkSheet.md` | 工作表操作（数据读写、行列操作、区域管理等） |

### 网页模块

| 模块 | 文件 | 功能描述 |
|------|------|----------|
| **Web** | `xbot.web.md` | 网页自动化基础功能 |
| **Browser** | `xbot.web.Browser.md` | 浏览器操作（导航、加载控制、元素查找等） |
| **Element** | `xbot.web.Element.md` | 网页元素操作（点击、输入、属性操作等） |

## 🚀 快速开始

### 1. 数据操作
```python
# 数据库操作
from xbot import ado
db = ado.Database()
db.open('连接字符串')
result = db.exec('SELECT * FROM table')
db.close()

# 数据表格操作
from xbot import app
app.databook.set_cell(1, 'A', 'Hello')
data = app.databook.get_row(1)
```

### 2. Excel自动化
```python
# Excel操作
from xbot import excel
workbook = excel.open('D:\\test.xlsx', kind='office')
worksheet = workbook.get_active_sheet()
worksheet.set_cell(1, 'A', 'Hello World')
workbook.save()
workbook.close()
```

### 3. 网页自动化
```python
# 网页操作
from xbot import web
browser = web.create('https://www.baidu.com', 'chrome')
browser.find('搜索框').input('影刀RPA')
browser.find('搜索按钮').click()
```

### 4. 日志记录
```python
# 日志记录
import xbot
xbot.logging.info('程序开始执行')
xbot.logging.error('发生错误')
```

## 📋 功能分类

### 数据处理
- **数据库操作**：连接、查询、执行SQL
- **数据表格**：读写、行列操作、区域管理
- **资源文件**：文本/二进制读写、文件复制

### 办公自动化
- **Excel处理**：工作簿/工作表操作、数据透视表、宏执行
- **对话框交互**：消息提示、确认对话框、自定义表单

### 网页自动化
- **浏览器控制**：导航、加载管理、JavaScript执行
- **元素操作**：点击、输入、选择、属性操作
- **数据提取**：表格抓取、网络监听

### 系统功能
- **日志记录**：多级别日志输出
- **元素选择**：网页/软件元素定位
- **图像识别**：图像元素选择器

## 🔧 使用建议

1. **Excel操作**：优先使用Office模式，功能最全面
2. **网页自动化**：Chrome浏览器兼容性最好
3. **数据库操作**：记得及时关闭连接
4. **错误处理**：使用logging模块记录关键信息
5. **元素定位**：建议使用元素库管理选择器

## 📖 详细文档

每个模块的详细API文档请参考对应的markdown文件，包含：
- 完整的参数说明
- 详细的代码示例
- 执行逻辑说明
- 注意事项和最佳实践

---

*本文档基于影刀RPA平台API整理，如有疑问请参考官方文档或联系技术支持。*
