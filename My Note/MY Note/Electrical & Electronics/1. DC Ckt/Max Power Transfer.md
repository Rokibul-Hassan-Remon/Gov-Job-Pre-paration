bnb# Statement of Theorem

একটি linear DC network যদি Thevenin equivalent এ convert করা হয়:

- Source voltage = $$V_{th}​$$
- Series resistance = $$R_{th}​$$

এবং load = $$R_L​$$

তাহলে load এ maximum power যাবে যখন:

$$R_L = R_{th}​$$

---

# Step 1: Equivalent Circuit

```txt
 Vth ---- Rth ---- RL
```

এখানে current পুরো loop এ same:

$$I = \frac{V_{th}}{R_{th}+R_L} (Ohm’s Law)$$

---

# Step 2: Load Power Formula

Load resistor এ power:

$$P_L = I^2 R_L$$

Current substitute করি:

$$P_L = \left(\frac{V_{th}}{R_{th}+R_L}\right)^2 R_L​$$

Simplify:

$$P_L = \frac{V_{th}^2 R_L}{(R_{th}+R_L)^2}​​$$

এটাই load power as function of RLR_LRL​

---

# Step 3: Maximum খুঁজবো

Maximum value বের করতে derivative নিতে হয়:

$$\frac{dP_L}{dR_L}=0$$

কারণ highest point এ slope zero হয়।

---

# Step 4: Differentiate

$$P_L = \frac{V_{th}^2 R_L}{(R_{th}+R_L)^2}​​$$

এখানে $$V_{th}^2​  (constant)$$ তাই ignore করা যায়।

Differentiate করলে result আসে:

$$\frac{dP_L}{dR_L}=\frac{V_{th}^2(R_{th}-R_L)}{(R_{th}+R_L)^3}​$$

এখন maximum এর জন্য:

$$\frac{dP_L}{dR_L}=0$$

Denominator zero হতে পারে না, তাই numerator zero:

$$Rth−RL=0$$

So:

$$RL=Rth​$$

**Proved.**

---

# Step 5: এটা Maximum নাকি Minimum?

দেখি behavior:

- যদি `RL<Rth`​ → derivative positive → power বাড়ছে
- যদি `RL>Rth​` → derivative negative → power কমছে

মানে আগে বাড়ে, পরে কমে।

তাই peak point = maximum।

---

# Step 6: Maximum Power কত?

`RL=Rth​` বসাই:

$$P_{max}=\frac{V_{th}^2}{4R_{th}}​​$$

---

# Intuition Proof (No Calculus)

Power depends on two opposite things:

## RL বাড়ালে:

- Load voltage বাড়ে
- কিন্তু current কমে

## RL কমালে:

- Current বাড়ে
- কিন্তু load voltage কমে

এই দুইয়ের perfect balance point:

```txt
			RL = Rth
```

---

# Engineer Insight

এটা কোনো magic না।

এটা simply:

> Voltage gain vs Current loss এর optimization point

---

# Final Proof Summary

We started from:

- Ohm's Law
- Power Formula
- Differentiation

And naturally got:

```text
			RL = Rth
```

