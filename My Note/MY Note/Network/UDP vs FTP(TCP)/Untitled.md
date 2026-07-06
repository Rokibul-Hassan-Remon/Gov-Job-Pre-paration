
*আমরা জানি যে video এবং audio পাঠানোর জন্য UDP দ্রুততর। কিন্তু যখন আমি FTP সম্পর্কে দেখলাম, তখন জানতে পারলাম যে FTP, TCP connection-এর উপর তৈরি। আমরা জানি FTP-ও অনেক দ্রুত কাজ করে। তাহলে FTP-কে TCP-এর পরিবর্তে UDP-এর উপর কেন তৈরি করা হলো না?*

 এখানে একটা misconception আছে:

> **FTP fast ≠ TCP fast**
> 
> FTP অনেক সময় **high throughput** দিতে পারে, কিন্তু সেটা **TCP-এর reliability** এর কারণে, UDP-এর মতো low-latency হওয়ার কারণে না।

---

# প্রথমে TCP vs UDP-এর আসল পার্থক্য

ধর, ১০০০টা packet আছে।

## TCP

TCP বলে

> "আমি প্রতিটা packet ঠিকমতো পৌঁছাবে নিশ্চিত করব।"

যদি packet 230 হারিয়ে যায়

```
1
2
3
...
229

230   (Lost)

231
232
```

Receiver বলবে

```
I only received up to 229.
Please resend 230.
```

Sender আবার পাঠাবে।

TCP features

- ACK
    
- Retransmission
    
- Ordering
    
- Congestion Control
    
- Flow Control
    

এগুলো করতে overhead লাগে।

---

## UDP

UDP বলে

```
Here are the packets.

Good luck.
```

No ACK

No retransmission

No ordering

No congestion control

তাই latency খুব কম।

---

# তাহলে FTP কেন TCP ব্যবহার করে?

কারণ FTP-এর জন্য speed-এর চেয়ে correctness বেশি গুরুত্বপূর্ণ।

ধরো তুমি

```
2GB Movie
```

download করছ।

যদি UDP ব্যবহার করো

```
Packet 50 lost

Packet 600 lost

Packet 1000 lost
```

Movie corrupt হয়ে যাবে।

তুমি চাইবে না।

তাই FTP বলে

```
Every byte must arrive.
```

এই জন্য TCP।

---

# কিন্তু FTP তো অনেক fast!

হ্যাঁ।

কারণ

```
High Throughput
```

এবং

```
Low Latency
```

এক জিনিস না।

---

## ধরো

তোমার highway

```
8 lane
```

একবার গাড়ি চলা শুরু করলে

```
1000 trucks
```

একসাথে যেতে পারে।

Throughput অনেক।

কিন্তু

প্রথম truck destination-এ পৌঁছাতে

১০ মিনিট লাগে।

Latency বেশি।

---

TCP অনেকটা এমন।

---

# ভিডিওতে কেন UDP?

ধরো তুমি YouTube Live দেখছ।

Frame

```
1
2
3
4
5
```

Frame 3 হারিয়ে গেল।

TCP হলে

```
Stop.

Wait.

Resend frame 3.
```

ভিডিও freeze করবে।

UDP হলে

```
Frame 3 gone?

No problem.

Play frame 4.
```

User বুঝতেই পারে না।

---

# এখন আসল প্রশ্ন

> Why not build UDP on top of TCP?

এখানে একটা logical contradiction আছে।

UDP-এর philosophy

```
Send immediately.
Don't wait.
```

TCP-এর philosophy

```
Wait until everything is correct.
```

অর্থাৎ

UDP যদি TCP-এর উপর চলে

```
UDP packet
        ↓
TCP
        ↓
IP
```

তাহলে TCP আগে থেকেই করবে

- ordering
    
- ACK
    
- retransmission
    
- congestion control
    

ফলে UDP আর UDP থাকবে না।

---

# Example

ধরো UDP packet

```
Packet A
Packet B
Packet C
```

TCP sequence বানাবে

```
Seq 1
Seq 2
Seq 3
```

যদি

```
Seq 2
```

হারিয়ে যায়

TCP বলবে

```
Wait.

Don't deliver Seq 3.
```

এটাকেই বলে

**Head-of-Line Blocking**

যেটা UDP এড়াতে চায়।

---

# আরেকটা কারণ

TCP already provides

- Reliable delivery
    
- Ordered delivery
    
- Error recovery
    

UDP এগুলোর কোনোটাই দেয় না।

যদি UDP-কে TCP-এর উপর বসাও

```
UDP
↓

TCP
```

UDP-এর আর কোনো কাজই থাকবে না।

এটা অনেকটা এমন:

```
Helmet
↓

Another Helmet
↓

Head
```

দুইটা helmet পরলে দ্বিতীয় helmet নতুন কোনো সুবিধা দিচ্ছে না।

---

# কিন্তু TCP-এর উপর অন্য protocol তো চলে?

হ্যাঁ।

অনেক protocol চলে।

```
HTTP
HTTPS
FTP
SMTP
IMAP
POP3
SSH
Telnet
```

কারণ এরা **application protocols**।

তারা TCP-এর reliable stream ব্যবহার করে নিজেদের application-level কাজ করে।

Layer:

```
Application
    HTTP
    FTP
    SMTP
        ↓
Transport
    TCP
        ↓
IP
```

---

# UDP-এর উপরও protocol চলে

যেমন

- DNS
    
- DHCP
    
- RTP
    
- TFTP
    
- QUIC (transport-like protocol over UDP)
    

কারণ এদের latency বা custom reliability দরকার।

---

# সবচেয়ে গুরুত্বপূর্ণ বিষয়

UDP এবং TCP দুটোই **Transport Layer Protocol**।

OSI/TCP-IP stack-এ তারা একই layer-এ থাকে:

```
Application
    HTTP
    FTP
    DNS
        ↓
Transport
 ┌───────────┐
 │ TCP  UDP  │
 └───────────┘
        ↓
IP
```

একই layer-এর একটি protocol সাধারণভাবে আরেকটি transport protocol-এর "উপর" তৈরি করা হয় না। Application protocol (যেমন FTP) TCP বা UDP-এর উপর চলে, কিন্তু UDP TCP-এর উপর চলে না।

### সংক্ষেপে

- **FTP TCP-এর উপর চলে**, কারণ ফাইলে একটি byte-ও হারানো চলবে না।
    
- **UDP TCP-এর উপর চলে না**, কারণ TCP-এর reliability, ordering এবং retransmission UDP-এর low-latency বৈশিষ্ট্যকে নষ্ট করে দেবে।
    
- **TCP এবং UDP প্রতিদ্বন্দ্বী transport protocol**, parent-child সম্পর্কের protocol নয়। তাই একটিকে আরেকটির উপর বসানোর কোনো বাস্তব সুবিধা নেই।