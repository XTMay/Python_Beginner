# CA03: Class Activities 20%

## Question 3: Grade Calculator (Covers 1.1–1.3) – 20%

**Objective:** Practice input/output, variables, expressions, flow control, and weighted calculations.

---

## Task:

Write a Python program that:

- Asks the user to enter three scores:
  - Homework score (0-100)
  - Midterm exam score (0-100)
  - Final exam score (0-100)
- Calculates the weighted total score using the formula:
  - **Total = Homework × 0.3 + Midterm × 0.3 + Final × 0.4**
- Displays an appropriate letter grade based on the total score:
  - 90-100 → "A" (Excellent)
  - 80-89 → "B" (Good)
  - 70-79 → "C" (Average)
  - 60-69 → "D" (Pass)
  - 0-59 → "F" (Fail)

---

## Requirements:

- Use `input()` and `print()`.
- Include at least one conditional (if-elif-else).
- Handle invalid inputs gracefully (e.g., non-numeric values).
- Validate that all scores are between 0 and 100.
- Calculate weighted average correctly (weights must sum to 100%).

---

## You are required to submit:

### 1. Python File (.py):

**a. Your complete working program saved in a file named:**
   - `yourname_grade_calculator.py`

**b. Make sure your code:**
   - Uses functions (`calculate_final_score`, `get_letter_grade`, `main`)
   - Includes proper input validation (0-100 range)
   - Has **if-elif-else** statements for decision making
   - Displays scores with two decimal places
   - Uses proper formatting with f-strings (e.g., `f"{score:.2f}"`)
   - Shows weight percentages clearly

**c. Test cases:**
   - A normal case (e.g., HW=85, Mid=78, Final=90)
   - Edge cases (e.g., exactly 90, 80, 70, or 60)
   - Invalid inputs (e.g., "abc", -10, 150)

---

### 2. Code Requirements

**Make sure your code includes:**

1. A function to calculate the weighted final score.
2. A function to determine the letter grade and comment.
3. Use of `input()` and `print()`.
4. Proper formatting using f-strings (e.g., `f"{score:.2f}"`).
5. Flow control (`if`, `elif`, `else`).
6. **Error handling with `try` and `except`.**
7. Input validation (checking 0-100 range).

---

## Grading Criteria:

| Criterion | Points |
|-----------|--------|
| Program runs correctly | 5 |
| Proper use of functions | 4 |
| Weighted calculation correct | 3 |
| Conditional logic (if-elif-else) | 3 |
| Input validation and error handling | 3 |
| Code formatting and comments | 2 |
| **Total** | **20** |

---

## Example Run:

```
============================================================
Grade Calculator / 成绩计算器
============================================================

权重分配 (Weights):
  - 作业 (Homework):  30%
  - 期中 (Midterm):   30%
  - 期末 (Final):     40%

Enter homework score (0-100): 85
Enter midterm score (0-100): 78
Enter final exam score (0-100): 90

============================================================
RESULTS / 结果
============================================================
作业成绩 (Homework):   85.00 (权重: 30%)
期中成绩 (Midterm):    78.00 (权重: 30%)
期末成绩 (Final):      90.00 (权重: 40%)
------------------------------------------------------------
总分 (Total Score):    84.90
等级 (Letter Grade):   B
评价 (Comment):        Good
============================================================
```

---

## Common Mistakes to Avoid:

1. **Weight Error**: Make sure weights add up to 100% (0.3 + 0.3 + 0.4 = 1.0).
2. **Simple Average**: Don't use `(hw + mid + fin) / 3` — this is wrong! Use weighted average.
3. **Operator Precedence**: Use parentheses when needed: `(a + b + c) / 3` not `a + b + c / 3`.
4. **Boundary Conditions**: Test scores at exactly 90, 80, 70, and 60.
5. **Range Validation**: Check that all scores are between 0 and 100.
6. **Comparison Operators**: Use `>=` not `>` for grade boundaries (90 should be an A).

---

## Formula Verification:

For homework=80, midterm=80, final=80:
```
Total = 80 × 0.3 + 80 × 0.3 + 80 × 0.4
      = 24 + 24 + 32
      = 80
```

For homework=90, midterm=80, final=85:
```
Total = 90 × 0.3 + 80 × 0.3 + 85 × 0.4
      = 27 + 24 + 34
      = 85
```

---

## Tips:

1. Start with the basic version without functions.
2. Test the weighted calculation by hand first.
3. Verify that weights sum to 1.0 (or 100%).
4. Then refactor your code to use functions.
5. Add error handling and input validation.
6. Test edge cases (boundary values like 90, 80, etc.).
7. Use f-strings for formatted output: `f"{value:.2f}"` for 2 decimal places.

---

## Advanced Extension (Optional, Extra Credit +5):

Add functionality to:
1. Calculate and display GPA (A=4.0, B=3.0, C=2.0, D=1.0, F=0.0)
2. Suggest what score is needed on the final exam to achieve a target grade
3. Add support for plus/minus grades (A+, A, A-, B+, etc.)

---

**Good luck!**
