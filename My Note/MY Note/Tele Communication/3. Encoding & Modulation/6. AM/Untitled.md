
# STEP 1 — Start with AM equation

$$s(t)=A_c(1+m\cos(2\pi f_m t))\cos(2\pi f_c t)$$

---

# STEP 2 — Expand the equation

প্রথমে multiply করি:

# Equation
$$s(t)

A_c\cos(2\pi f_c t)  
+  
mA_c\cos(2\pi f_m t)\cos(2\pi f_c t)  $$


এখন trig identity use করি:

$$\cos A\cos B=\frac{1}{2}[\cos(A+B)+\cos(A-B)]$$

তাহলে:

$$s(t)

A_c\cos(2\pi f_c t)  
+  
\frac{mA_c}{2}\cos2\pi(f_c+f_m)t  
+  
\frac{mA_c}{2}\cos2\pi(f_c-f_m)t  $$


---

# STEP 3 — এখন প্রতিটা part আলাদা করি

---

# PART 1 — Carrier

$$A_c\cos(2\pi f_c t)  $$

Frequency spectrum:

```text
Amplitude
      ^
Ac/2  |                    Ac/2
      |                    ↑
------+--------------------|-----------------> f
                           fc
```

👉 এখানে only carrier frequency আছে।

---

# PART 2 — Upper Sideband (USB)

$$\frac{mA_c}{2}\cos2\pi(f_c+f_m)t  $$

Spectrum:

```text
Amplitude
      ^
mAc/4 |                           mAc/4
      |                           ↑
------+---------------------------|---------> f
                               fc+fm
```

👉 এটা carrier-এর উপরে shift হয়েছে।

---

# PART 3 — Lower Sideband (LSB)

$$\frac{mA_c}{2}\cos2\pi(f_c-f_m)t  $$

Spectrum:

```text
Amplitude
      ^
|     |                mA_c/4
      |                ↑
------+----------------|-------------------> f
                     fc-fm
```

👉 এটা carrier-এর নিচে shift হয়েছে।

---

# STEP 4 — সবগুলো একসাথে combine করি

Final AM spectrum:

```text
Amplitude
  |                                       ↑[s(f)]
  |                                       |
  |         ↑          ↑        ↑         |                ↑           ↑         ↑
  |  		|		   |	    |         |                |           |         |
  |        mAc/4	  Ac/2 	  mAc/4		  |              mAc/4       Ac/2      mAc/4
--|---------|----------|--------|---------+----------------|-----------|----------|--------> f
		 -fc+fm	      -fc       -fc-fm                   fc-fm         fc       fc+fm
		   USB		 Carrier	  LSB                      LSB        Carrier      USB
```

---

# STEP 5 — এখন bandwidth calculate করি

Bandwidth মানে:

> highest frequency − lowest frequency

---

## Highest frequency


$$f_c+f_m  $$


---

## Lowest frequency


$$f_c-f_m  $$

---

# STEP 6 — Subtract করি

$$BW=(f_c+f_m)-(f_c-f_m)$$

Expand:


$$BW=f_c+f_m-f_c+f_m  $$



$$BW=2f_m  $$


---

# FINAL RESULT

`BW=2f_m`

---

# MOST IMPORTANT INTUITION

Message frequency ($f_m$):

- একবার carrier-এর উপরে যায়
    
- একবার carrier-এর নিচে যায়
    

তাই total spread হয়:


$$2f_m  $$

---

# FINAL MEMORY MAP

```text
Carrier:
fc

Sidebands:
fc+fm
fc-fm

Bandwidth:
(fc+fm) - (fc-fm)

= 2fm
```

