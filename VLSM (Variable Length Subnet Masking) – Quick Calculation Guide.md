# VLSM (Variable Length Subnet Masking) – Quick Calculation Guide

## Scenario

You are a Network Administrator.

Your company has been assigned the network:

```text
10.0.0.0/16
```

You need to create separate subnets for different departments.

| Department | Required Hosts |
| ---------- | -------------: |
| DEP        |             60 |
| HR         |             25 |
| Finance    |             12 |
| Sales      |              5 |

---

# Step 1: Arrange in Descending Order

Always allocate the largest subnet first.

| Department | Hosts |
| ---------- | ----: |
| DEP        |    60 |
| HR         |    25 |
| Finance    |    12 |
| Sales      |     5 |

---

# Step 2: Add 2

Why?

* 1 Network Address
* 1 Broadcast Address

Formula

```text
Required Hosts + 2
```

| Department | Hosts | +2 | Total Needed |
| ---------- | ----: | -: | -----------: |
| DEP        |    60 |  2 |           62 |
| HR         |    25 |  2 |           27 |
| Finance    |    12 |  2 |           14 |
| Sales      |     5 |  2 |            7 |

---

# Step 3: Find the Next Power of 2

## Power of 2 Cheat Sheet

```text
2² = 4
2³ = 8
2⁴ = 16
2⁵ = 32
2⁶ = 64
2⁷ = 128
2⁸ = 256
2⁹ = 512
2¹⁰ = 1024
```

### Trick

Keep doubling.

```text
2
4
8
16
32
64
128
256
512
1024
```

Now compare:

```text
62 → 64
27 → 32
14 → 16
7  → 8
```

---

# Step 4: Convert to Prefix

## Prefix Cheat Sheet

| Total Addresses | Prefix | Usable Hosts |
| --------------: | :----: | -----------: |
|               4 |   /30  |            2 |
|               8 |   /29  |            6 |
|              16 |   /28  |           14 |
|              32 |   /27  |           30 |
|              64 |   /26  |           62 |
|             128 |   /25  |          126 |
|             256 |   /24  |          254 |
|             512 |   /23  |          510 |
|            1024 |   /22  |         1022 |

Therefore

| Department | Total Addresses | Prefix |
| ---------- | --------------: | :----: |
| DEP        |              64 |   /26  |
| HR         |              32 |   /27  |
| Finance    |              16 |   /28  |
| Sales      |               8 |   /29  |

---

# Step 5: Allocate the Subnets

Given Network

```text
10.0.0.0/16
```

---

## Department (60 Hosts)

```
Network ID      : 10.0.0.0/26
First Host      : 10.0.0.1
Last Host       : 10.0.0.62
Broadcast       : 10.0.0.63
```

Next Available Network

```
10.0.0.64
```

---

## HR (25 Hosts)

```
Network ID      : 10.0.0.64/27
First Host      : 10.0.0.65
Last Host       : 10.0.0.94
Broadcast       : 10.0.0.95
```

Next Available Network

```
10.0.0.96
```

---

## Finance (12 Hosts)

```
Network ID      : 10.0.0.96/28
First Host      : 10.0.0.97
Last Host       : 10.0.0.110
Broadcast       : 10.0.0.111
```

Next Available Network

```
10.0.0.112
```

---

## Sales (5 Hosts)

```
Network ID      : 10.0.0.112/29
First Host      : 10.0.0.113
Last Host       : 10.0.0.118
Broadcast       : 10.0.0.119
```

---

# Final VLSM Table

| Department | Hosts | Needed (+2) | Total Addresses | Prefix | Network ID | First Host | Last Host  | Broadcast  |
| ---------- | ----: | ----------: | --------------: | :----: | ---------- | ---------- | ---------- | ---------- |
| DEP        |    60 |          62 |              64 |   /26  | 10.0.0.0   | 10.0.0.1   | 10.0.0.62  | 10.0.0.63  |
| HR         |    25 |          27 |              32 |   /27  | 10.0.0.64  | 10.0.0.65  | 10.0.0.94  | 10.0.0.95  |
| Finance    |    12 |          14 |              16 |   /28  | 10.0.0.96  | 10.0.0.97  | 10.0.0.110 | 10.0.0.111 |
| Sales      |     5 |           7 |               8 |   /29  | 10.0.0.112 | 10.0.0.113 | 10.0.0.118 | 10.0.0.119 |

---

# Interview Shortcut (Fastest Method)

Most network engineers don't calculate powers every time.

They simply memorize this table:

| Need Hosts | Choose Prefix |
| ---------: | :-----------: |
|        ≤ 2 |      /30      |
|        ≤ 6 |      /29      |
|       ≤ 14 |      /28      |
|       ≤ 30 |      /27      |
|       ≤ 62 |      /26      |
|      ≤ 126 |      /25      |
|      ≤ 254 |      /24      |
|      ≤ 510 |      /23      |
|     ≤ 1022 |      /22      |

### Examples

```
Need 60 hosts?
60 ≤ 62
Answer = /26

Need 25 hosts?
25 ≤ 30
Answer = /27

Need 12 hosts?
12 ≤ 14
Answer = /28

Need 5 hosts?
5 ≤ 6
Answer = /29
```

No calculations required.

---

# One-Minute VLSM Formula

```text
1. Sort the host requirements (Largest → Smallest)

2. Add 2
   (Network + Broadcast)

3. Find the next power of 2

4. Match it with the prefix

5. Allocate subnets sequentially
```

---

# Memory Cheat Sheet

## Powers of Two

```text
2
4
8
16
32
64
128
256
512
1024
2048
4096
```

## Prefix Cheat Sheet

```text
/30 → 4 addresses → 2 usable
/29 → 8 addresses → 6 usable
/28 → 16 addresses → 14 usable
/27 → 32 addresses → 30 usable
/26 → 64 addresses → 62 usable
/25 → 128 addresses → 126 usable
/24 → 256 addresses → 254 usable
/23 → 512 addresses → 510 usable
/22 → 1024 addresses → 1022 usable
```

---

# Final Answer for the Scenario

```
Given Network : 10.0.0.0/16

DEP      → 10.0.0.0/26
HR       → 10.0.0.64/27
Finance  → 10.0.0.96/28
Sales    → 10.0.0.112/29
```

This is the standard VLSM allocation method used in networking certifications (CCNA/CCNP), interviews, and enterprise network design.
