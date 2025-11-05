# CA04: Class Activities 20%

## Question 4: Currency Converter (Covers 1.1–1.3) – 20%

**Objective:** Practice input/output, variables, expressions, flow control, and data structures (dictionaries).

---

## Task:

Write a Python program that:

- Asks the user to enter an amount in USD (US Dollars).
- Asks the user to choose a target currency from the following options:
  - **CNY** (Chinese Yuan) - Rate: 6.45
  - **EUR** (Euro) - Rate: 0.85
  - **GBP** (British Pound) - Rate: 0.73
  - **JPY** (Japanese Yen) - Rate: 110.0
  - **USD** (US Dollar) - Rate: 1.0 (base currency)
- Converts the USD amount to the target currency using the formula:
  - **Converted Amount = USD Amount × Exchange Rate**
- Displays the conversion result with proper formatting.

---

## Requirements:

- Use `input()` and `print()`.
- Store exchange rates in a **dictionary** data structure.
- Include at least one conditional (if-elif-else) OR use dictionary lookup.
- Handle invalid inputs gracefully:
  - Non-numeric amounts
  - Negative amounts
  - Unsupported currency codes
- Convert currency codes to uppercase (accept both "cny" and "CNY").
- Display all supported currencies to the user.

---

## You are required to submit:

### 1. Python File (.py):

**a. Your complete working program saved in a file named:**
   - `yourname_currency_converter.py`

**b. Make sure your code:**
   - Uses a **dictionary** to store exchange rates
   - Uses functions (`convert_currency`, `display_available_currencies`, `main`)
   - Includes proper input validation
   - Handles case-insensitive currency codes (CNY, cny, Cny all work)
   - Has **if-elif-else** statements OR dictionary lookup for decision making
   - Displays amounts with two decimal places
   - Uses proper formatting with f-strings (e.g., `f"{amount:.2f}"`)

**c. Test cases:**
   - A normal case (e.g., 100 USD to CNY)
   - Different currency codes (EUR, GBP, JPY)
   - Lowercase currency input (e.g., "eur")
   - Invalid currency code (e.g., "XYZ")
   - Invalid amount (e.g., "abc", negative number)

---

### 2. Code Requirements

**Make sure your code includes:**

1. A **dictionary** to store exchange rates and currency names.
2. A function to convert USD to target currency.
3. A function to display all supported currencies.
4. Use of `input()` and `print()`.
5. Proper formatting using f-strings (e.g., `f"{amount:.2f}"`).
6. Flow control (`if`, `elif`, `else`) OR dictionary `.get()` / `in` operator.
7. **Error handling with `try` and `except`.**
8. String methods (`.upper()`, `.strip()`).

---

## Grading Criteria:

| Criterion | Points |
|-----------|--------|
| Program runs correctly | 4 |
| Proper use of dictionary | 4 |
| Proper use of functions | 3 |
| Input validation | 3 |
| String handling (case-insensitive) | 2 |
| Error handling (try-except) | 2 |
| Code formatting and comments | 2 |
| **Total** | **20** |

---

## Example Run:

```
============================================================
Currency Converter / 货币转换器
Convert USD to other currencies
============================================================

============================================================
支持的货币 (Supported Currencies):
============================================================
  CNY  : 人民币 (Chinese Yuan)       (1 USD =    6.45 CNY)
  EUR  : 欧元 (Euro)                  (1 USD =    0.85 EUR)
  GBP  : 英镑 (British Pound)         (1 USD =    0.73 GBP)
  JPY  : 日元 (Japanese Yen)          (1 USD =  110.00 JPY)
  USD  : 美元 (US Dollar)             (1 USD =    1.00 USD)
============================================================

Enter amount in USD: 100
Enter target currency code (e.g., CNY, EUR, GBP): CNY

============================================================
CONVERSION RESULT / 转换结果
============================================================
原始金额 (Amount):      100.00 USD
目标货币 (Currency):    CNY - 人民币 (Chinese Yuan)
汇率 (Exchange Rate):   1 USD = 6.45 CNY
------------------------------------------------------------
结果 (Result):          645.00 CNY
============================================================
```

---

## Common Mistakes to Avoid:

1. **Formula Error**: Use multiplication (`amount * rate`), not division.
2. **Case Sensitivity**: Convert input to uppercase: `currency.upper()`.
3. **Dictionary Errors**: Check if key exists before accessing: `if currency in rates:`
4. **No Validation**: Validate amount is positive and numeric.
5. **Poor Error Messages**: Tell users which currencies are supported when they enter invalid code.

---

## Dictionary Structure Example:

```python
EXCHANGE_RATES = {
    "CNY": {"rate": 6.45, "name": "人民币 (Chinese Yuan)"},
    "EUR": {"rate": 0.85, "name": "欧元 (Euro)"},
    "GBP": {"rate": 0.73, "name": "英镑 (British Pound)"},
    "JPY": {"rate": 110.0, "name": "日元 (Japanese Yen)"},
    "USD": {"rate": 1.0, "name": "美元 (US Dollar)"}
}
```

---

## Tips:

1. Start with a simple dictionary of rates.
2. Use `.upper()` to handle case-insensitive input.
3. Use `if currency in EXCHANGE_RATES:` to check validity.
4. Show the list of supported currencies at the beginning.
5. Test with various inputs including invalid ones.
6. Use f-strings for formatted output: `f"{value:.2f}"` for 2 decimal places.

---

## Advanced Extension (Optional, Extra Credit +5):

Add functionality to:
1. Support bidirectional conversion (CNY → USD, EUR → GBP, etc.)
2. Calculate and display transaction fees (e.g., 2% fee)
3. Compare historical exchange rates
4. Create a conversion table showing 100 USD in all currencies

---

**Good luck!**
