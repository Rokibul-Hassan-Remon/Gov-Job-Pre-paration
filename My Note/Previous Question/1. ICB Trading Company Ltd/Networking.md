 This is a **VLSM (Variable Length Subnet Mask)** problem.

---

# Step 1: Given Network

Network:

```
192.198.10.0/22
```

### What does /22 mean?

```
Subnet Mask

255.255.252.0
```

Total IPs:

$$2^{32-22}=2^{10}=1024  $$

Usable Hosts:

$$1024-2=1022  $$

Network Range: **(192.198.8.0  -  192.198.11.255)**


> **Note:** Although the question writes **192.198.10.0/22**, the actual **network address** of that /22 block is **192.198.8.0/22** because /22 networks increment by 4 in the third octet (0, 4, 8, 12, ...).

---

# Step 2: Arrange Departments in Descending Order

Always allocate the **largest subnet first**.

| Department     | Hosts |
| -------------- | ----: |
| Finance        |   250 |
| Administration |   250 |
| Accounting     |   125 |
| Management     |   120 |
| IT             |    60 |

---

# Step 3: Determine Required Prefix

## Finance (250)

Need

```
250 + 2 = 252 IPs
```

Next power of 2

```
256
```

```
Therefore CIDR:
/24
```

```
Subnet Mask  : 255.255.255.0
```


---

## Administration (250)

Also

```
/24
```

Subnet Mask

```
255.255.255.0
```

---

## Accounting (125)

Need

```
125+2=127
```

Next power

```
128
```

```
/25
```

Mask

```
255.255.255.128
```

---

## Management (120)

Need

```
122
```

Next power

```
128
```

```
/25
```

Mask:

```
255.255.255.128
```

---

## IT (60)

Need

```
62
```

Next power

```
64
```

```
/26
```

Mask

```
255.255.255.192
```

---

# Step 4: Allocate Addresses

Start from the beginning of the available /22 block.

---

## Finance
Needs /24

```
Network
192.198.8.0/24
```

Range :

```
192.198.8.1  -  192.198.8.254
```

Broadcast :

```
192.198.8.255
```

---

## Administration

Next /24 :

```
Network

192.198.9.0/24
```

Hosts : 

```
192.198.9.1 -  192.198.9.254
```

Broadcast :

```
192.198.9.255
```

---

## Accounting

Next /25

```
192.198.10.0/25
```

Hosts 

```
192.198.10.1 - 192.198.10.126
```

Broadcast

```
192.198.10.127
```

---

## Management

Next /25

```
192.198.10.128/25
```

Hosts

```
192.198.10.129 - 192.198.10.254
```

Broadcast

```
192.198.10.255
```

---

## IT

Next /26

```
192.198.11.0/26
```

Hosts : 

```
192.198.11.1  -  192.198.11.62
```

Broadcast

```
192.198.11.63
```

---

# Final Answer

| Department     | Hosts Needed | Prefix | Subnet Mask     | Network Address    | Valid Host Range                | Broadcast Address |
| -------------- | -----------: | ------ | --------------- | ------------------ | ------------------------------- | ----------------- |
| Finance        |          250 | /24    | 255.255.255.0   | **192.198.8.0**    | 192.198.8.1 – 192.198.8.254     | 192.198.8.255     |
| Administration |          250 | /24    | 255.255.255.0   | **192.198.9.0**    | 192.198.9.1 – 192.198.9.254     | 192.198.9.255     |
| Accounting     |          125 | /25    | 255.255.255.128 | **192.198.10.0**   | 192.198.10.1 – 192.198.10.126   | 192.198.10.127    |
| Management     |          120 | /25    | 255.255.255.128 | **192.198.10.128** | 192.198.10.129 – 192.198.10.254 | 192.198.10.255    |
| IT             |           60 | /26    | 255.255.255.192 | **192.198.11.0**   | 192.198.11.1 – 192.198.11.62    | 192.198.11.63     |

---

## Address Space Utilization

The allocated subnets consume:

- Finance: 256 IPs
    
- IT: 256 IPs
    
- Administration: 128 IPs
    
- Accounting: 128 IPs
    
- HR: 64 IPs
    

Total used:


$$256 + 256 + 128 + 128 + 64 = 832 \text{ IPs}  $$


Available in the /22 block:

$$1024 - 832 = 192 \text{ IPs}  $$
These remaining IPs are from **192.198.11.64** through **192.198.11.255**, which can be reserved for future expansion.