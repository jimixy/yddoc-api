# xbot.ado 模块

## 描述

ADO 接口主要是针对数据的操作，如数据库的连接/断开、SQL 语句的执行。

## 类

### `Database`

数据库操作类，用于连接、操作和关闭数据库。

## 方法

### `open(conn_str)`

连接数据库。

**参数：**
- `conn_str`：数据库连接字符串。关于数据库连接字符串的获取，可以进入连接数据库操作文档查看细节部分

**返回值：**
- 无

**示例：**
```python
from xbot import ado

def main(args):
    db = ado.Database()
    db.open('数据库连接字符串')
```

**执行逻辑：** 获取已配置好的数据库 → 连接数据库

---

### `exec(sql, timeout_seconds=20)`

执行 SQL 语句。

**参数：**
- `sql`：SQL 语句
- `timeout_seconds`：SQL 语句执行超时时间，默认超时时间为 20 秒

**返回值：**
- `List[any]`：返回 SQL 语句执行结果

**示例：**
```python
from xbot import ado

def main(args):
    db = ado.Database()
    result = db.exec('select * from table_A')
    print(result)
```

**执行逻辑：** 获取已配置好的数据库 → 执行 SQL 语句 → 输出执行结果

---

### `close()`

关闭数据库连接。

**参数：**
- 无

**返回值：**
- 无

**示例：**
```python
from xbot import ado

def main(args):
    db = ado.Database()
    db.close()
```

**执行逻辑：** 获取已配置好的数据库 → 关闭数据库

## 使用流程

典型的数据库操作流程：

1. **创建数据库实例**：`db = ado.Database()`
2. **连接数据库**：`db.open(conn_str)`
3. **执行 SQL 操作**：`result = db.exec(sql)`
4. **关闭连接**：`db.close()`
