# xbot.logging 模块

## 描述

用来记录程序运行中的日志信息，如：错误信息，调试信息，警告信息，普通信息。

## 方法

### `debug(text)`

记录 Debug（调试）日志信息。

**参数：**
- `text`：要记录的日志信息

**返回值：**
- 无

**示例：**
```python
import xbot

def main(args):
    xbot.logging.debug('hello world')
```

**执行逻辑：** 将调试信息"hello world"打印在运行日志中

---

### `info(text)`

记录普通日志信息。

**参数：**
- `text`：需要记录的日志信息

**返回值：**
- 无

**示例：**
```python
import xbot

def main(args):
    xbot.logging.info('hello world')
```

**执行逻辑：** 将普通信息"hello world"打印在运行日志中

---

### `warning(text)`

记录警告日志信息。

**参数：**
- `text`：需要记录的日志信息

**返回值：**
- 无

**示例：**
```python
import xbot

def main(args):
    xbot.logging.warning('hello world')
```

**执行逻辑：** 将警告信息"hello world"打印在运行日志中

---

### `error(text)`

记录错误日志信息。

**参数：**
- `text`：需要记录的日志信息

**返回值：**
- 无

**示例：**
```python
import xbot

def main(args):
    xbot.logging.error('hello world')
```

**执行逻辑：** 将错误信息"hello world"打印在运行日志中

## 日志级别说明

| 方法 | 级别 | 用途 |
|------|------|------|
| `debug()` | DEBUG | 调试信息，用于开发调试 |
| `info()` | INFO | 普通信息，记录程序运行状态 |
| `warning()` | WARNING | 警告信息，需要注意但不影响程序运行 |
| `error()` | ERROR | 错误信息，程序出现错误时记录 |
