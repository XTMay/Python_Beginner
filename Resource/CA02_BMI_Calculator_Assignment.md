# CA02: Class Activities 20%

## Question 2: BMI Calculator (Covers 1.1–1.3) – 20%

**Objective:** Practice input/output, variables, expressions, and flow control.

---

## Task:

Write a Python program that:

- Asks the user to enter their weight in kilograms (kg).
- Asks the user to enter their height in meters (m).
- Calculates the BMI using the formula:
  - **BMI = weight / (height × height)**
- Displays an appropriate health category based on the BMI value:
  - Below 18.5 → "Underweight"
  - Between 18.5 and 24.9 → "Normal weight"
  - Between 25.0 and 29.9 → "Overweight"
  - Above 30.0 → "Obese"

---

## Requirements:

- Use `input()` and `print()`.
- Include at least one conditional (if-elif-else).
- Handle invalid inputs gracefully (e.g., non-numeric values, negative numbers).
- Validate that height and weight are positive numbers.
- Check if height is reasonable (warn if > 3m, as user may have entered cm instead of m).

---

## You are required to submit:

### 1. Python File (.py):

**a. Your complete working program saved in a file named:**
   - `yourname_bmi_calculator.py`

**b. Make sure your code:**
   - Uses functions (`calculate_bmi`, `get_bmi_category`, `main`)
   - Includes proper input validation
   - Has **if-elif-else** statements for decision making
   - Displays BMI with two decimal places
   - Uses proper formatting with f-strings (e.g., `f"{bmi:.2f}"`)

**c. Test cases:**
   - A normal case (e.g., 70kg, 1.75m)
   - An edge case (e.g., BMI = 18.5 or 25.0)
   - An invalid input (e.g., "hello", negative number, or height > 3m)

---

### 2. Code Requirements

**Make sure your code includes:**

1. A function to calculate BMI from weight and height.
2. A function to determine BMI category.
3. Use of `input()` and `print()`.
4. Proper formatting using f-strings (e.g., `f"{bmi:.2f}"`).
5. Flow control (`if`, `elif`, `else`).
6. **Error handling with `try` and `except`.**

---

## Grading Criteria:

| Criterion | Points |
|-----------|--------|
| Program runs correctly | 5 |
| Proper use of functions | 4 |
| Input validation | 3 |
| Conditional logic (if-elif-else) | 3 |
| Error handling (try-except) | 3 |
| Code formatting and comments | 2 |
| **Total** | **20** |

---

## Example Run:

```
==========================================================
BMI Calculator / BMI计算器
==========================================================

Enter your weight in kilograms (kg): 70
Enter your height in meters (m): 1.75

------------------------------------------------------------
Weight (体重):        70.0 kg
Height (身高):        1.75 m
BMI:                  22.86
Category (分类):      Normal weight
------------------------------------------------------------
```

---

## Common Mistakes to Avoid:

1. **Formula Error**: Make sure to use `height ** 2` or `height * height`, not just `height`.
2. **Type Error**: Remember to convert input strings to float: `float(input(...))`.
3. **Range Check**: Validate that weight and height are positive.
4. **Height Unit Warning**: Check if height > 3m (user may have entered cm).
5. **Boundary Values**: Test BMI values at exactly 18.5, 25.0, and 30.0.

---

## Tips:

1. Start with the basic version without functions.
2. Then refactor your code to use functions.
3. Finally, add error handling with try-except.
4. Test your program with various inputs, including invalid ones.
5. Use f-strings for formatted output: `f"{value:.2f}"` for 2 decimal places.

---

**Good luck!**
