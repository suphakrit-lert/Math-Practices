# 1. Probability
- **ไล่ Probability แต่ละตัว & คิด Sample Space แต่ละตัวให้ถูก!!!**
- Law of Total Probability: เศษกับตัวนึงของส่วนจะเหมือนกัน
- Check Sample Space!
- Check: Sample X elements, One at a time?, With replacement?
- **ส่วนมาก Dice/Card จะเป็นลำดับ จับ one-by-one**
- Pair of Card:
  ```
  - First Card can be anything (52/52) 
  - Second card has to be paired (12/51) 
  - So P = (52/52)(12/51)
  ```
- Pair of Q: Probability of choosing 2 queens out of a deck of cards 
$$ P(A) = \frac{4}{52} \cdot \frac{3}{51} $$
**Dependence: คิด Sample Space ของแต่ละตัวที่จับให้ถูก ตัวแรกเลือกจับได้ 52 ใบ ตัวสองเลือกจับได้แค่ 51 ใบ**
- **Exact Face/Number: ได้หน้าเป๊ะ = คิดแยก 3 เคส เคส1: ซ้ายหน้าเป๊ะ, เคส2: ขวาหน้าเป๊ะ, เคส3: ทั้งคู่หน้าเป๊ะ**

Let's say you have 2 dice. What is the probability of getting at least one 4? A = [X][4] or [4][X] or [4][4]
$$
P(A)=\frac{5}{6} \cdot \frac{1}{6}+\frac{1}{6} \cdot \frac{5}{6}+\frac{1}{6} \cdot \frac{1}{6}
$$

If you roll a dice three times, what is the probability to get two consecutive threes?
$$
\begin{aligned}
& A=[3][3][X] \text { or }[X][3][3] \text { or }[3][3][3] \\
& \qquad P(A)=\left(\frac{1}{6}\right)^2 \cdot \frac{5}{6} \cdot 2+\left(\frac{1}{6}\right)^3=\frac{11}{216}
\end{aligned}
$$

- **Complementary**
```
*AT LEAST* two N from has X ⟺ 1 - None of N has X
```

- Birthday Problem is PAIRING Problem: Pair first, second, ...
Room $\mathrm{w} / n \mathrm{ppl}$, Find prob of at least two ppl have same birthday
$\mathrm{A}=$ Event that at least two ppl have same birthday
$\mathrm{A}^{\mathrm{c}}=$ Event that no one shares same birthday

$$
P(A)=1-P\left(A^c\right)=1-\frac{365 \times 364 \times \ldots \times(365-n+1)}{365^n}
$$


- Binomial Distribution 

According to hospital records, 75% of patients suffering from a disease die from that disease. Find out the probability that 4 out of the 6 randomly selected patients survive.
$$ P(A)=\binom{6}{4}(0.25)^4(0.75)^2 $$

- Two RV Multiplications -> Use Tower Rules

# 2. Statistics
- **Hypothesis Testing: Calculate the test statistics $Z_0$ first**
- Left-skew = ข้อสอบกระจอกที่ทุกคนทำได้
  - Mean (คนโง่ดึงคะแนนลง) < Median (คนปกติทำได้) < Mode (คนปกติทำได้เยอะ)
- Right-skew = รวยกระจุกจนกระจาย
  - Mean (คนรวยดึงมีน) > Median (คนปกติจน) > Mode (คนปกติสุดๆจนมาก)
- Sample Proportion SD: $\sigma=p(1-p)$
- CI of Proportion RV

  Let's say the population on Facebook clicks ads with a clickthrough-rate of $p$. We select a sample of size $N$ and examine the sample's conversion rate, denoted by $\hat{p}$, what is the minimum sample size $N$ such that $\mathrm{P}(|\hat{p}-p|<\delta)=95 \%$ ?
Tips: Sample Proportion SD: $\sigma=p(1-p)$

$$
\begin{gathered}
P\left(|Z|<Z_{1-\frac{\alpha}{2}}\right)=1-\alpha=0.95 \\
\mathrm{P}(|\hat{p}-p|<\delta)=95 \% \\
\mathrm{P}\left(\frac{|\hat{p}-p|}{\sqrt{\operatorname{Var}(p)}}<\frac{\delta}{\sqrt{\operatorname{Var}(p)}}\right)=95 \% \\
\mathrm{P}\left(|Z|<\frac{\delta}{\sqrt{\operatorname{Var}(p)}}\right)=95 \% \\
\frac{\delta}{\sqrt{\operatorname{Var}(p)}}=Z_{1-\frac{\alpha}{2}}=1.96 \\
\frac{\delta \cdot \sqrt{n}}{\sigma}=1.96 \\
\sqrt{n}=1.96 \frac{\sigma}{\delta} \\
\text { Sample Proportion: } \sigma=p(1-p) \\
n=\left(1.96 \frac{p(1-p)}{\delta}\right)^2
\end{gathered}
$$

- CI of Binomial distribution

Confidence Interval: Binomial Distribution There are 100 products and 25 of them are bad. What is the confidence interval?
$X$ is the RV for number of bad products from 100 products

$$
\begin{gathered}
P\left(|Z|<Z_{1-\frac{\alpha}{2}}\right)=1-\alpha \\
P\left(\left|\frac{X-\mathbb{E}[X]}{\sigma / \sqrt{n}}\right|<Z_{1-\frac{\alpha}{2}}\right)=1-\alpha \\
\mathbb{E}[X] \in\left[X-\frac{\sigma}{\sqrt{n}} \cdot Z_{1-\frac{\alpha}{2}}, X+\frac{\sigma}{\sqrt{n}} \cdot Z_{1-\frac{\alpha}{2}}\right] \\
\mathbb{E}[X] \in\left[X-\frac{n p(1-p)}{\sqrt{n}} \cdot Z_{1-\frac{\alpha}{2}}, X+\frac{n p(1-p)}{\sqrt{n}} \cdot Z_{1-\frac{\alpha}{2}}\right] \\
\mathbb{E}[X] \in\left[25-\frac{100 \cdot 0.25(0.75)}{\sqrt{100}} \cdot 1.96,25+\frac{100 \cdot 0.25(0.75)}{\sqrt{100}} \cdot 1.96\right] \\
\mathbb{E}[X] \in[25-3.675,25+3.675]
\end{gathered}
$$

- A/B testing: is a controlled experiment that compares two or more versions of a component to determine which performs better based on specific metrics

# 3. SQL
- **Pivot: Summarize rows to columns** with `sum(case when col = ‘val1’ then 1 else 0 end) as val1_count` to create a new column
- Find duplicate:
  ```sql
  select count(dup_col) 
  group by 1, 2, 3 
  having count(dup_col) > 1
  ```
- Handle duplicate data in SQL
  ```
  1.	Select Distinct
  2.	GROUP BY
  3.	Unique Key 
  4.	Delete duplicated data
  ```

- Tip: Histogram = Double group by:
  - 1st group by: Count the frequency of each category in CTE 
  - 2nd group by: Create frequency histogram
- Rolling Avg: 
  ```sql
  avg(col) over (
    partition by id 
    order by date 
    rows between 1 preceding 
    and 1 following
  )
  ```
- Date difference between two rows:
  ```sql
  select max(date) – min(date) as date_diff
  from source_table
  group by id
  ```
- Transaction Order:
  ```sql
  rank over (
    partition by id 
    order by date asc
  ) as ranking
  ```
- Whenever the question asks about finding “0 values,” e.g., users or neighborhoods, start thinking LEFT JOIN
  ```sql
  SELECT neighborhoods.name
  FROM neighborhoods
  LEFT JOIN users
    ON neighborhoods.id = users.neighborhood_id
  WHERE users.id IS NULL
  ```
- Lag()
  ```sql
  lags(col, 1, 0) over (partition by col) as new_col
  ```
- Tips: Indexes = Lookup Table 1) Retrieve data faster 2) Reduce Disc Access
- CAST before doing the date part 
  ```dql
  date_part('day', transaction date::date)
  ```
# 4. Algorithms
- Maximizing Profit: Loop one time, Find the min_price and max_profit (price - min_price, max_profit) at each turn
  ```py
  for price in prices:
      min_value = min(min_value, price)
      max_profit = max(max_profit, price - min_value)
  print(max_profit)
  ```
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
  ```py
  while i < n1 and j < n2:
      if list1[i] < list2[j]:
          merged_list.append(list1[i])
          i += 1
      else:
          merged_list.append(list2[j])
          j += 1

  if i < n1:
      merged_list.extend(list1[i:])
  elif j < n2:
      merged_list.extend(list2[j:])
  ```
- Number Complement:
  - Work with bit -> Use bit operation
  - Complement of Number: `num.bit_length() -> mask = (1 << bit_length) - 1 -> num ^ mask`
- Remove Element: Remove elements by `list.remove(num)`
- Subsequence Check: Double pointer
  ```py
  while i < len(s) and j < len(t):
      if s[i] == t[j]:
          i += 1
      j += 1

  i == len(s)
  ```

- String2 (`bba`, 2 `b`) Cover String1 (`b`, 1 `b`) if `string1_dict - string2_dict == {}`
  ```py
  from collections import Counter
  string1_dict = Counter(string1)
  string2_dict = Counter(string2)
  string1_dict - string2_dict == {}
  ```

- Merge Intervals: if next_start <= current_end, update current_end to max(current_end, next_end)
  ```py
  merged_intervals = [intervals[0]]

  for i in range(1, len(intervals)):
      if intervals[i][0] <= merged_intervals[-1][1]:
          merged_intervals[-1][1] = max(merged_intervals[-1][1], intervals[i][1])
      else:
          merged_intervals.append(intervals[i])
  ```

- Summary Range: Convert to interval first
  ```py
  nums = [0, 2, 3, 4, 6, 8, 9]
  ranges = []
  for num in nums:
      if ranges and ranges[-1][1] == num - 1:
          ranges[-1][1] = num
      else:
          ranges.append([num, num])
  ```

- Check One-to-One Mapping:
  ```py
  for (x, y) in zip(pattern, s):
      if x in mapper.keys():
          if mapper[x] != y:
              return False
      else:
          mapper[x] = y
  ```

- Advanced Stocking Selling: Use GREEDY algorithm. Find max and sell immediately
  ```py
  start = prices[0]
  max = 0
  n = len(prices)

  for i in range(1, n):
      if start < prices[i]:
          max += prices[i] - start
      
      start = prices[i]
  ```

- Remove duplicated from the sorted array: Double pointers
  ```py
  nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
  n = len(nums)

  j = 1

  for i in range(1, n):
      if nums[i] != nums[j - 1]:
          nums[j] = nums[i]
          j += 1
  ```

- Needle in a Haystack
  ```py
  n_needle = len(needle)
  n_haystack = len(haystack)

  if n_haystack < n_needle:
      return -1

  for i in range(0, n_haystack):
      if haystack[i:i+n_needle] == needle:
          return i
  ```

- Rotate Array: Use Modulo
  ```py
  # Time Complexity: O(n)
  # Space Complexity: O(n)
  nums = [1, 2, 3, 4, 5, 6, 7]
  k = 3

  n = len(nums)
  k = k % n
  rotated = [0] * n

  for i in range(n):
      rotated[(i + k) % n] = nums[i]

  for i in range(n):
      nums[i] = rotated[i]
  ```
# 5. ML
