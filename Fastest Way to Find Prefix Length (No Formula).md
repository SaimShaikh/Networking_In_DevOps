# Fastest Way to Find Prefix Length (No Formula)

This is the easiest method used in interviews, CCNA exams, and by many network engineers.

---

# The Only Table You Need to Memorize

| Prefix | Total Addresses | Usable Hosts |
| :----: | --------------: | -----------: |
|   /30  |               4 |            2 |
|   /29  |               8 |            6 |
|   /28  |              16 |           14 |
|   /27  |              32 |           30 |
|   /26  |              64 |           62 |
|   /25  |             128 |          126 |
|   /24  |             256 |          254 |
|   /23  |             512 |          510 |
|   /22  |            1024 |         1022 |

---

# Memory Trick

Just remember this single line:

```text
/24 → 254 hosts
/25 → 126 hosts
/26 → 62 hosts
/27 → 30 hosts
/28 → 14 hosts
/29 → 6 hosts
/30 → 2 hosts
```

Notice the pattern:

* Prefix increases by **1**
* Available hosts become **approximately half**

Example:

```text
/24 → 254
        ↓
/25 → 126
        ↓
/26 → 62
        ↓
/27 → 30
        ↓
/28 → 14
        ↓
/29 → 6
        ↓
/30 → 2
```

---

# How to Find the Prefix

Simply compare the required hosts with the **Usable Hosts** column.

Choose the **first value that is greater than or equal to** your requirement.

---

## Example 1

Requirement:

```text
60 Hosts
```

Compare:

```text
30 ❌ Too small

62 ✅ Fits
```

Answer

```text
Prefix = /26
```

---

## Example 2

Requirement

```text
25 Hosts
```

Compare

```text
14 ❌

30 ✅
```

Answer

```text
Prefix = /27
```

---

## Example 3

Requirement

```text
12 Hosts
```

Compare

```text
6 ❌

14 ✅
```

Answer

```text
Prefix = /28
```

---

## Example 4

Requirement

```text
5 Hosts
```

Compare

```text
2 ❌

6 ✅
```

Answer

```text
Prefix = /29
```

---

## Example 5

Requirement

```text
90 Hosts
```

Compare

```text
62 ❌

126 ✅
```

Answer

```text
Prefix = /25
```

---

## Example 6

Requirement

```text
200 Hosts
```

Compare

```text
126 ❌

254 ✅
```

Answer

```text
Prefix = /24
```

---

## Example 7

Requirement

```text
500 Hosts
```

Compare

```text
254 ❌

510 ✅
```

Answer

```text
Prefix = /23
```

---

# Practice Questions

| Required Hosts | Prefix |
| -------------: | :----: |
|              3 |   /29  |
|              5 |   /29  |
|             10 |   /28  |
|             20 |   /27  |
|             45 |   /26  |
|             80 |   /25  |
|            150 |   /24  |
|            300 |   /23  |
|            700 |   /22  |

---

# 5-Second Interview Shortcut

1. Look at the number of required hosts.
2. Find the **first usable host value** that is **greater than or equal to** the requirement.
3. The corresponding prefix is your answer.

Example:

```text
Need 45 hosts?

30 ❌

62 ✅

Answer = /26
```

Example:

```text
Need 180 hosts?

126 ❌

254 ✅

Answer = /24
```

---

# One-Line Cheat Sheet

```text
2  → /30
6  → /29
14 → /28
30 → /27
62 → /26
126 → /25
254 → /24
510 → /23
1022 → /22
```

---

# Golden Rule

> **Find the first usable host value that is greater than or equal to the required number of hosts. The corresponding prefix is the correct subnet mask.**

This is the quickest method because there is **no need to calculate powers of 2, subtract from 32, or use formulas**. It is the technique most networking professionals use for fast subnetting during interviews and day-to-day network design.
