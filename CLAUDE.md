# 编码原则（极简版）

## 核心理念

**快速失败 > 完美代码**
**函数式 > 面向对象**
**直接明了 > 优雅抽象**
**少写代码 > 多写代码**

---

## 1. Fast-Fail 原则

### 错误处理：默认不处理

```python
✅ 好：让错误直接抛出
def get_user(user_id):
    return db.query('SELECT * FROM users WHERE id = ?', [user_id])

❌ 坏：捕获后不知道怎么办
def get_user(user_id):
    try:
        return db.query(...)
    except Exception as e:
        print(f'Error: {e}')  # 然后呢？
        return None  # 隐藏了问题
```

### 必须包含的错误信息

- 文件名、函数名
- 输入参数（完整的，不要省略）
- 失败原因（具体的，不要模糊）
- 上下文数据

```python
# 好的错误
raise Exception(f"Failed to process user {user_id} in process_payment(): {reason}")

# 差的错误
raise Exception("Processing failed")
```

---

## 2. 代码风格：越简单越好

### 默认用函数，不用类

```python
✅ 好：直接函数
def calculate_total(items):
    return sum(item.price for item in items)

❌ 坏：无谓的封装
class Calculator:
    def __init__(self):
        pass

    def calculate_total(self, items):
        return sum(item.price for item in items)
```

### 函数保持简短（< 20 行）

- 超过 20 行 = 拆分信号
- 一个函数只做一件事
- 能看到底层实现，不要超过 3 层调用

### 重复好过错误的抽象

```python
✅ 好：重复但清晰
def create_user(data):
    return db.query('INSERT INTO users ...', [data['name'], data['email']])

def create_post(data):
    return db.query('INSERT INTO posts ...', [data['title'], data['content']])

❌ 坏：过早抽象
def create(table, data):  # 看起来灵活，实际脆弱
    keys = ','.join(data.keys())
    values = list(data.values())
    return db.query(f'INSERT INTO {table} ({keys}) VALUES (?)', values)
```

### 变量命名要完整

```python
✅ user_email, post_title, total_price
❌ e, t, p
```

### Python 惯用法（Pythonic）

```python
# 用列表推导式/生成器，不用循环
✅ result = [x * 2 for x in items if x > 0]
✅ total = sum(item.price for item in items)

❌ result = []
   for x in items:
       if x > 0:
           result.append(x * 2)

# 用 f-string，不用旧式格式化
✅ f"User {user_id} failed: {reason}"
❌ "User %s failed: %s" % (user_id, reason)
❌ "User {} failed: {}".format(user_id, reason)

# 直接返回布尔值
✅ return age >= 18
✅ return name in valid_names

❌ if age >= 18:
       return True
   else:
       return False

# 用 with 管理资源，不要手动 close
✅ with open('file.txt') as f:
       data = f.read()

❌ f = open('file.txt')
   data = f.read()
   f.close()

# 用字典的 get()，不要 try-except KeyError
✅ value = data.get('key', default_value)
✅ value = data.get('key')  # 返回 None 如果不存在

❌ try:
       value = data['key']
   except KeyError:
       value = default_value
```

---

## 3. 测试原则

### 真实测试，禁止 mock

```python
✅ 好：调用真实 API
def test_create_user():
    user = api.create_user({'name': 'test', 'email': 'test@example.com'})
    assert user['id'] is not None

❌ 坏：mock 一切
def test_create_user():
    mock_db.query.return_value = {'id': 1}
    user = create_user(...)
    assert mock_db.query.called  # 测了个寂寞
```

### 测试要简单直接

- 一个测试一个断言
- 测试名称要描述场景
- 遇错即停，不要 try-catch

---

## 4. 工作流程

### 简化版（3 步）

1. **写测试** - 用真实依赖
2. **写实现** - 最简单能跑的版本
3. **检查错误信息** - 确保出错时能快速定位

### 遇到问题：3 次规则

- 尝试 3 次还不行 → 停下来
- 记录尝试过的方案和错误
- 换一个完全不同的思路
- 或者直接问人

---

## 5. 禁止清单

### 永远不要

- ❌ **创建 utils/helpers 文件夹** - 会变成垃圾场
- ❌ **写 wrapper 函数** - 直接调用底层库
- ❌ **提前抽象** - 至少重复 3 次再考虑
- ❌ **捕获异常后不处理** - 要么处理，要么别捕获
- ❌ **封装 logger** - print() 就够了
- ❌ **超过 3 层的抽象** - 你在炫技

### 提交前检查（3 项）

- [ ] 能编译/运行
- [ ] 有测试且通过
- [ ] 错误信息清晰（手动触发一个错误看看）

---

## 6. 决策原则（遇到多个方案时）

问自己 3 个问题：

1. **哪个最简单？** - 选最简单的
2. **哪个代码最少？** - 选代码最少的
3. **出错时哪个更容易调试？** - 选容易调试的

如果还是不确定 → 选第一个想到的方案，不要过度思考

---

## 7. 配置说明

### 语言和输出

- **思考过程**：用英文
- **回复内容**：用中文

### 项目相关（根据实际项目填写）

- **技术栈**：[在这里填写]
- **关键联系人**：[在这里填写]
- **常见问题**：[在这里填写]

---

## 记住

**写代码不是为了炫技，是为了解决问题**

- 代码越少，bug 越少
- 抽象越少，调试越快
- 功能能用就行，不要追求完美
- 3 个月后的你会感谢现在写简单代码的你
