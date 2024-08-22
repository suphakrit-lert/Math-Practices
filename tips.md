# 1. Probability
- Law of Total Probability: เศษกับตัวนึงของส่วนจะเหมือนกัน


# 2. Statistics
- Hypothesis Testing: Calculate the test statistics $Z_0$ first

# 3. SQL
- **Pivot: Summarize rows to columns** with `sum(case when col = ‘val1’ then 1 else 0 end) as val1_count` to create a new column
- Find duplicate -> `select count(dup_col) group by 1, 2, 3 having count(dup_col) > 1`
- Tip: Histogram = Double group by:
  - 1st group by: Count the frequency of each category in CTE 
  - 2nd group by: Create frequency histogram
- Rolling Avg: `avg(col) over (partition by id order by date rows between 1 preceding and 1 following)`
- Date difference between two rows:  `... group by id & max(date) – min(date)`
- Transaction Order: `rank over (partition by id order by date asc) as ranking`

# 4. Algorithms
- Maximizing Profit: Loop one time, Find the min_price and max_profit (price - min_price, max_profit) at each turn
- Two Sum to Target: Find a complement (= target - cur_num) if the complement in the list or not
- Palindrome: `x == x[::-1]`
- Roman to Integer: Check with `s[i + 1]` but cap at `i < n - 1`
  ```py
  for i in range(n):
      if (i < n - 1) and (value_mapping[s[i]] < value_mapping[s[i + 1]]):
          value -= value_mapping[s[i]]
      else:
          value += value_mapping[s[i]]
  ```
- Longest Common Prefix: Sort first then compare the first and last elements
- Valid Parentheses: Use stack
  ```py
  # len(stack) == 0: The stack with opening bracket should not be empty for a closing bracket
  # c != mapper[stack.pop()]: The popped opening bracket should match the closing one
  for c in s:
      if c in mapper.keys():
          stack.append(c)
      elif len(stack) == 0 or c != mapper[stack.pop()]:
          print(False)
          break
  ```
- Merge Two Sorted Lists: double pointer + `while i < n1 and j < n2`

# 5. ML
