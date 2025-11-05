# Python 错误类型复习资料

## 目录
1. [语法错误 (Syntax Error)](#1-语法错误-syntax-error)
2. [使用 try-except 处理输入错误](#2-使用-try-except-处理输入错误)
3. [输入验证与类型错误](#3-输入验证与类型错误)
4. [输出格式化与逻辑错误](#4-输出格式化与逻辑错误)
5. [综合练习题](#5-综合练习题)

---

## 1. 语法错误 (Syntax Error)

### 1.1 拼错关键字

#### ❌ 错误示例：
```python
# 拼错 print
pirnt("Hello World")

# 拼错 if
fi x > 5:
    print("大于5")

# 拼错 def
dfe my_function():
    print("函数")
```

#### ✅ 正确写法：
```python
print("Hello World")

if x > 5:
    print("大于5")

def my_function():
    print("函数")
```

**常见拼错关键字：**
- `pirnt` → `print`
- `fi` / `iff` → `if`
- `esle` → `else`
- `fro` / `ofr` → `for`
- `whlie` → `while`
- `dfe` → `def`
- `retrun` → `return`
- `improt` → `import`

---

### 1.2 缩进错误（空格位置错）

#### ❌ 错误示例：
```python
# 缺少缩进
if x > 5:
print("大于5")  # IndentationError

# 缩进不一致
def my_function():
    x = 5
        y = 10  # IndentationError（多了缩进）
    return x + y

# for循环缩进错误
for i in range(5):
print(i)  # IndentationError
```

#### ✅ 正确写法：
```python
# 正确缩进（4个空格或1个Tab）
if x > 5:
    print("大于5")

# 缩进一致
def my_function():
    x = 5
    y = 10
    return x + y

# for循环正确缩进
for i in range(5):
    print(i)
```

**缩进规则：**
- Python使用缩进来表示代码块
- 通常使用4个空格（推荐）或1个Tab
- 同一代码块必须使用相同的缩进
- `:` 后面的内容必须缩进

---

### 1.3 用错符号

#### ❌ 错误示例：
```python
# 用中文符号
print（"Hello"）  # SyntaxError：中文括号
x = 5；  # SyntaxError：中文分号

# 赋值符号错误
if x = 5:  # SyntaxError：应该用 ==
    print("等于5")

# 引号不匹配
name = "Alice'  # SyntaxError：开始是"，结束是'
message = 'Hello  # SyntaxError：缺少结束引号

# 冒号遗漏
if x > 5  # SyntaxError：缺少冒号
    print("大于5")

# 括号不匹配
result = (10 + 5  # SyntaxError：缺少右括号
```

#### ✅ 正确写法：
```python
# 使用英文符号
print("Hello")
x = 5

# 正确的比较符号
if x == 5:
    print("等于5")

# 引号匹配
name = "Alice"
message = 'Hello'

# 添加冒号
if x > 5:
    print("大于5")

# 括号匹配
result = (10 + 5)
```

**常见符号错误：**
| 错误 | 正确 | 说明 |
|------|------|------|
| `（）` | `()` | 中文括号 vs 英文括号 |
| `；` | `;` | 中文分号（Python通常不需要分号）|
| `：` | `:` | 中文冒号 vs 英文冒号 |
| `，` | `,` | 中文逗号 vs 英文逗号 |
| `"` `"` | `"` | 中文引号 vs 英文引号 |
| `if x = 5` | `if x == 5` | 赋值 vs 比较 |

---

## 2. 使用 try-except 处理输入错误

### 2.1 基本的 try-except 结构

```python
try:
    # 可能出错的代码
    dangerous_code()
except ErrorType:
    # 处理错误的代码
    handle_error()
```

### 2.2 处理数字输入错误

#### ❌ 没有错误处理：
```python
age = int(input("请输入你的年龄："))
print(f"你的年龄是：{age}")
# 如果用户输入 "abc"，程序会崩溃：ValueError
```

#### ✅ 使用 try-except：
```python
try:
    age = int(input("请输入你的年龄："))
    print(f"你的年龄是：{age}")
except ValueError:
    print("错误：请输入有效的数字！")
```

#### ✅✅ 更完善的处理（循环直到输入正确）：
```python
while True:
    try:
        age = int(input("请输入你的年龄："))
        if age < 0:
            print("年龄不能是负数，请重新输入！")
            continue
        if age > 150:
            print("年龄不合理，请重新输入！")
            continue
        print(f"你的年龄是：{age}")
        break
    except ValueError:
        print("错误：请输入有效的数字！")
```

### 2.3 处理多种类型的输入错误

```python
def get_number(prompt, min_value=None, max_value=None):
    """获取用户输入的数字，带有验证功能"""
    while True:
        try:
            value = float(input(prompt))

            # 检查范围
            if min_value is not None and value < min_value:
                print(f"错误：输入值不能小于 {min_value}")
                continue

            if max_value is not None and value > max_value:
                print(f"错误：输入值不能大于 {max_value}")
                continue

            return value

        except ValueError:
            print("错误：请输入有效的数字！")
        except KeyboardInterrupt:
            print("\n程序被用户中断")
            return None

# 使用示例
score = get_number("请输入分数（0-100）：", 0, 100)
if score is not None:
    print(f"你的分数是：{score}")
```

### 2.4 处理除零错误

```python
try:
    numerator = int(input("请输入分子："))
    denominator = int(input("请输入分母："))
    result = numerator / denominator
    print(f"结果是：{result}")
except ValueError:
    print("错误：请输入有效的整数！")
except ZeroDivisionError:
    print("错误：分母不能为零！")
except Exception as e:
    print(f"发生未知错误：{e}")
```

### 2.5 多个 except 块

```python
def safe_calculate():
    try:
        x = int(input("请输入第一个数字："))
        y = int(input("请输入第二个数字："))
        result = x / y
        print(f"结果：{result}")
    except ValueError:
        print("错误：输入必须是数字！")
    except ZeroDivisionError:
        print("错误：不能除以零！")
    except KeyboardInterrupt:
        print("\n用户取消操作")
    except Exception as e:
        print(f"未知错误：{e}")
    finally:
        print("计算结束")  # 无论是否出错都会执行

safe_calculate()
```

---

## 3. 输入验证与类型错误

### 3.1 字符串输入验证

```python
def get_name():
    """获取有效的姓名输入"""
    while True:
        name = input("请输入你的姓名：").strip()

        # 检查是否为空
        if not name:
            print("错误：姓名不能为空！")
            continue

        # 检查是否包含数字
        if any(char.isdigit() for char in name):
            print("错误：姓名不应该包含数字！")
            continue

        # 检查长度
        if len(name) < 2:
            print("错误：姓名至少需要2个字符！")
            continue

        return name

name = get_name()
print(f"欢迎，{name}！")
```

### 3.2 邮箱格式验证

```python
def get_email():
    """获取有效的邮箱输入"""
    while True:
        email = input("请输入邮箱地址：").strip()

        # 基本验证
        if not email:
            print("错误：邮箱不能为空！")
            continue

        if "@" not in email:
            print("错误：邮箱必须包含 @ 符号！")
            continue

        if email.count("@") > 1:
            print("错误：邮箱只能有一个 @ 符号！")
            continue

        if not "." in email.split("@")[1]:
            print("错误：邮箱格式不正确！")
            continue

        return email

email = get_email()
print(f"邮箱：{email}")
```

### 3.3 选项输入验证

```python
def get_choice(options):
    """获取有效的选项"""
    print("请选择：")
    for i, option in enumerate(options, 1):
        print(f"{i}. {option}")

    while True:
        try:
            choice = int(input("请输入选项编号："))
            if 1 <= choice <= len(options):
                return choice
            else:
                print(f"错误：请输入 1 到 {len(options)} 之间的数字！")
        except ValueError:
            print("错误：请输入有效的数字！")

# 使用示例
menu = ["开始游戏", "查看设置", "退出"]
user_choice = get_choice(menu)
print(f"你选择了：{menu[user_choice-1]}")
```

---

## 4. 输出格式化与逻辑错误

### 4.1 限制小数位数

#### 方法1：使用 f-string（推荐）

```python
# 保留2位小数
price = 19.9567
print(f"价格：${price:.2f}")  # 输出：价格：$19.96

# 保留0位小数（取整）
people_count = 15.7
print(f"人数：{people_count:.0f}")  # 输出：人数：16

# 保留3位小数
pi = 3.1415926
print(f"圆周率：{pi:.3f}")  # 输出：圆周率：3.142
```

#### 方法2：使用 round() 函数

```python
price = 19.9567
print(f"价格：${round(price, 2)}")  # 输出：价格：$19.96

people_count = 15.7
print(f"人数：{round(people_count)}")  # 输出：人数：16
```

#### 方法3：使用 format() 函数

```python
price = 19.9567
print("价格：${}".format(round(price, 2)))  # 输出：价格：$19.96
print("价格：${:.2f}".format(price))  # 输出：价格：$19.96
```

### 4.2 人数计算的逻辑错误处理

#### ❌ 错误示例：
```python
total_people = 10
buses = 3
people_per_bus = total_people / buses
print(f"每辆车：{people_per_bus} 人")  # 输出：3.3333... 人（不合理）
```

#### ✅ 正确处理：

```python
# 方法1：向上取整（确保所有人都有座位）
import math

total_people = 10
buses = 3

# 每辆车平均人数（向上取整）
people_per_bus = math.ceil(total_people / buses)
print(f"每辆车最多：{people_per_bus} 人")  # 输出：4 人

# 方法2：向下取整（只显示完整分配）
people_per_bus = total_people // buses  # 整除
remaining = total_people % buses  # 余数
print(f"每辆车：{people_per_bus} 人")
print(f"剩余：{remaining} 人")

# 方法3：完整的分配逻辑
def distribute_people(total, vehicles):
    """分配人数到车辆"""
    base = total // vehicles  # 基本人数
    extra = total % vehicles   # 额外人数

    result = []
    for i in range(vehicles):
        if i < extra:
            result.append(base + 1)  # 前几辆车多1人
        else:
            result.append(base)

    return result

total_people = 10
buses = 3
distribution = distribute_people(total_people, buses)

for i, count in enumerate(distribution, 1):
    print(f"第{i}辆车：{count}人")
# 输出：
# 第1辆车：4人
# 第2辆车：3人
# 第3辆车：3人
```

### 4.3 金额计算的格式化

```python
# 计算总价
price = 19.99
quantity = 3
total = price * quantity

# 格式化为货币格式
print(f"单价：${price:.2f}")
print(f"数量：{quantity}")
print(f"总计：${total:.2f}")

# 处理可能的浮点数误差
print(f"总计：${round(total, 2):.2f}")

# 更专业的货币格式
print(f"总计：${total:,.2f}")  # 千位分隔符：$1,234.56
```

### 4.4 百分比格式化

```python
# 计算百分比
correct = 85
total = 100
percentage = (correct / total) * 100

# 方法1：保留1位小数
print(f"正确率：{percentage:.1f}%")  # 85.0%

# 方法2：使用 % 格式符
print(f"正确率：{correct/total:.1%}")  # 85.0%

# 方法3：无小数
print(f"正确率：{percentage:.0f}%")  # 85%
```

### 4.5 对齐和填充

```python
# 左对齐
name = "Alice"
print(f"{name:<10}|")  # "Alice     |"

# 右对齐
print(f"{name:>10}|")  # "     Alice|"

# 居中
print(f"{name:^10}|")  # "  Alice   |"

# 用特定字符填充
print(f"{name:*^10}|")  # "**Alice***|"

# 数字格式化（补零）
number = 5
print(f"{number:03d}")  # "005"
```

---

## 5. 综合练习题

### 练习1：学生成绩管理系统

编写一个程序，要求：
1. 输入学生姓名（不能为空，不能包含数字）
2. 输入成绩（0-100之间的数字）
3. 如果输入错误，提示并重新输入
4. 计算等级（A: 90-100, B: 80-89, C: 70-79, D: 60-69, F: 0-59）
5. 输出格式化的结果

#### 参考答案：

```python
def get_student_name():
    """获取学生姓名"""
    while True:
        name = input("请输入学生姓名：").strip()

        if not name:
            print("错误：姓名不能为空！")
            continue

        if any(char.isdigit() for char in name):
            print("错误：姓名不应包含数字！")
            continue

        return name

def get_score():
    """获取成绩"""
    while True:
        try:
            score = float(input("请输入成绩（0-100）："))

            if score < 0 or score > 100:
                print("错误：成绩必须在0-100之间！")
                continue

            return score
        except ValueError:
            print("错误：请输入有效的数字！")

def calculate_grade(score):
    """计算等级"""
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

def main():
    """主程序"""
    print("=" * 40)
    print("学生成绩管理系统")
    print("=" * 40)

    name = get_student_name()
    score = get_score()
    grade = calculate_grade(score)

    print("\n" + "=" * 40)
    print("成绩报告")
    print("=" * 40)
    print(f"姓名：{name}")
    print(f"成绩：{score:.1f}")
    print(f"等级：{grade}")
    print("=" * 40)

if __name__ == "__main__":
    main()
```

---

### 练习2：计算器程序

编写一个简单的计算器，要求：
1. 输入两个数字
2. 选择运算符（+, -, *, /）
3. 处理所有可能的输入错误
4. 格式化输出结果（保留2位小数）
5. 特别处理除零错误

#### 参考答案：

```python
def get_number(prompt):
    """获取数字输入"""
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("错误：请输入有效的数字！")

def get_operator():
    """获取运算符"""
    valid_operators = ['+', '-', '*', '/']
    while True:
        operator = input("请输入运算符 (+, -, *, /)：").strip()
        if operator in valid_operators:
            return operator
        print(f"错误：请输入有效的运算符：{', '.join(valid_operators)}")

def calculate(num1, num2, operator):
    """执行计算"""
    try:
        if operator == '+':
            return num1 + num2
        elif operator == '-':
            return num1 - num2
        elif operator == '*':
            return num1 * num2
        elif operator == '/':
            if num2 == 0:
                raise ZeroDivisionError("不能除以零！")
            return num1 / num2
    except ZeroDivisionError as e:
        print(f"错误：{e}")
        return None

def main():
    """主程序"""
    print("=" * 40)
    print("简单计算器")
    print("=" * 40)

    num1 = get_number("请输入第一个数字：")
    operator = get_operator()
    num2 = get_number("请输入第二个数字：")

    result = calculate(num1, num2, operator)

    if result is not None:
        print("\n" + "=" * 40)
        print(f"{num1} {operator} {num2} = {result:.2f}")
        print("=" * 40)

if __name__ == "__main__":
    main()
```

---

### 练习3：班级人数分组

将班级学生分配到若干个小组，要求：
1. 输入总人数（必须是正整数）
2. 输入小组数量（必须是正整数）
3. 计算每组人数（整数）
4. 显示分配结果
5. 处理所有输入错误

#### 参考答案：

```python
def get_positive_integer(prompt):
    """获取正整数"""
    while True:
        try:
            value = int(input(prompt))
            if value <= 0:
                print("错误：请输入正整数！")
                continue
            return value
        except ValueError:
            print("错误：请输入有效的整数！")

def distribute_students(total_students, num_groups):
    """分配学生到小组"""
    if num_groups > total_students:
        print(f"警告：小组数量（{num_groups}）大于学生总数（{total_students}）")
        print("部分小组将为空")

    base_size = total_students // num_groups
    extra = total_students % num_groups

    groups = []
    for i in range(num_groups):
        if i < extra:
            groups.append(base_size + 1)
        else:
            groups.append(base_size)

    return groups

def main():
    """主程序"""
    print("=" * 40)
    print("班级分组系统")
    print("=" * 40)

    total_students = get_positive_integer("请输入班级总人数：")
    num_groups = get_positive_integer("请输入小组数量：")

    groups = distribute_students(total_students, num_groups)

    print("\n" + "=" * 40)
    print("分组结果")
    print("=" * 40)
    print(f"总人数：{total_students}人")
    print(f"小组数：{num_groups}组")
    print("-" * 40)

    for i, size in enumerate(groups, 1):
        print(f"第{i:2d}组：{size:3d}人")

    print("=" * 40)
    print(f"验证：{sum(groups)}人（应等于{total_students}人）")

if __name__ == "__main__":
    main()
```

---

### 练习4：商品购物车

编写一个购物车程序，要求：
1. 可以添加商品（名称和价格）
2. 价格必须是正数，保留2位小数
3. 计算总价
4. 显示每件商品和总价（格式化输出）
5. 处理所有输入错误

#### 参考答案：

```python
def get_product_name():
    """获取商品名称"""
    while True:
        name = input("请输入商品名称（或输入'q'结束）：").strip()

        if name.lower() == 'q':
            return None

        if not name:
            print("错误：商品名称不能为空！")
            continue

        return name

def get_price():
    """获取商品价格"""
    while True:
        try:
            price = float(input("请输入商品价格：$"))

            if price <= 0:
                print("错误：价格必须大于0！")
                continue

            return price
        except ValueError:
            print("错误：请输入有效的数字！")

def display_cart(cart):
    """显示购物车"""
    if not cart:
        print("购物车是空的！")
        return

    print("\n" + "=" * 50)
    print("购物车清单")
    print("=" * 50)
    print(f"{'序号':<5} {'商品名称':<20} {'价格':>10}")
    print("-" * 50)

    total = 0
    for i, (name, price) in enumerate(cart, 1):
        print(f"{i:<5} {name:<20} ${price:>9.2f}")
        total += price

    print("=" * 50)
    print(f"{'总计':>25} ${total:>9.2f}")
    print("=" * 50)

def main():
    """主程序"""
    cart = []

    print("=" * 50)
    print("购物车系统")
    print("=" * 50)
    print("提示：输入'q'结束添加商品\n")

    while True:
        name = get_product_name()

        if name is None:
            break

        price = get_price()
        cart.append((name, price))
        print(f"✓ 已添加：{name} - ${price:.2f}\n")

    display_cart(cart)

if __name__ == "__main__":
    main()
```

---

## 6. 常见错误速查表

### 语法错误 (SyntaxError)

| 错误代码 | 原因 | 解决方法 |
|---------|------|---------|
| `if x = 5:` | 使用赋值符号而非比较符号 | 改为 `if x == 5:` |
| `if x > 5` | 缺少冒号 | 改为 `if x > 5:` |
| `print("hello"` | 缺少右括号 | 改为 `print("hello")` |
| `pirnt("hello")` | 拼写错误 | 改为 `print("hello")` |

### 缩进错误 (IndentationError)

| 错误代码 | 原因 | 解决方法 |
|---------|------|---------|
| `if x > 5:`<br>`print(x)` | 缺少缩进 | 添加4个空格缩进 |
| 混用Tab和空格 | 缩进不一致 | 统一使用4个空格 |

### 类型错误 (TypeError / ValueError)

| 错误代码 | 原因 | 解决方法 |
|---------|------|---------|
| `int("abc")` | 无法转换为整数 | 使用try-except处理 |
| `10 / 0` | 除以零 | 检查分母或使用try-except |

---

## 7. 调试技巧

### 7.1 使用 print() 调试

```python
def calculate_average(numbers):
    print(f"Debug: 输入的数字列表 = {numbers}")  # 调试输出

    total = sum(numbers)
    print(f"Debug: 总和 = {total}")  # 调试输出

    count = len(numbers)
    print(f"Debug: 数量 = {count}")  # 调试输出

    average = total / count
    print(f"Debug: 平均值 = {average}")  # 调试输出

    return average
```

### 7.2 使用 try-except-else-finally

```python
try:
    # 尝试执行的代码
    file = open("data.txt", "r")
    data = file.read()
except FileNotFoundError:
    # 文件不存在时的处理
    print("文件不存在！")
except PermissionError:
    # 没有权限时的处理
    print("没有读取权限！")
else:
    # 没有异常时执行
    print("文件读取成功！")
    print(data)
finally:
    # 无论是否异常都执行（清理资源）
    try:
        file.close()
        print("文件已关闭")
    except:
        pass
```

---

## 8. 考前检查清单

在考试前，确保你能够：

- [ ] 正确使用Python关键字（if, for, while, def等）
- [ ] 使用正确的缩进（4个空格）
- [ ] 区分赋值（=）和比较（==）
- [ ] 使用英文符号而非中文符号
- [ ] 使用try-except处理输入错误
- [ ] 验证输入类型（int, float, str）
- [ ] 使用f-string格式化输出（{value:.2f}）
- [ ] 处理整数除法和余数（//, %）
- [ ] 正确处理小数位数（人数用整数）
- [ ] 使用while循环重复获取有效输入

---

## 祝你考试顺利！🎉

记住：
1. **仔细检查拼写和符号**
2. **使用try-except保护输入**
3. **验证输入的有效性**
4. **格式化输出结果**
5. **测试边界情况**
