# MixLoRA Evaluation Results

This file documents real inference behavior of the MixLoRA system, showing:

* Learned adapter routing
* Mixed-skill generation
* Practical business scenarios

---

## 1. Customer Support Triage

**Input**

> I waited 3 days for delivery. The product quality is good but your support team never replied. Can you summarize my issue and mention the overall sentiment?

**Predicted Routing**

| Adapter   | Weight |
| --------- | ------ |
| Sentiment | 0.45   |
| Summary   | 0.55   |

**Model Output**

> The customer reports delayed delivery and lack of support response while acknowledging good product quality, reflecting mixed but slightly negative sentiment.

**Observation**

* Model combined summarization + tone detection
* Correctly captured conflicting aspects

---

## 2. App Review Digest

**Input**

> Summarize this app review in one line: The UI looks beautiful and payments are smooth, but the app crashes frequently on Android 13 and notifications don’t work.

**Routing**

| Adapter   | Weight |
| --------- | ------ |
| Sentiment | 0.20   |
| Summary   | 0.80   |

**Output**

> The app offers great design and payments but suffers from crashes and broken notifications on Android.

**Observation**

* Summary-dominant routing
* Preserved critical negatives

---

## 3. Sentiment Classification

**Input**

> I’m extremely disappointed. I paid for premium but got basic features.

**Routing**

| Adapter   | Weight |
| --------- | ------ |
| Sentiment | 0.92   |
| Summary   | 0.08   |

**Output**

> The text expresses strong negative sentiment and frustration.

**Observation**

* Pure sentiment behavior
* Near one-hot routing

---

## 4. Balanced Product Feedback

**Input**

> The laptop performance is great for coding, but the battery barely lasts 3 hours.

**Routing**

| Adapter   | Weight |
| --------- | ------ |
| Sentiment | 0.50   |
| Summary   | 0.50   |

**Output**

> Good performance but poor battery life, indicating mixed sentiment.

**Observation**

* True mixed-skill generation
* Demonstrates MixLoRA objective

---

## 5. Business Communication

**Input**

> Client liked the demo but is worried about pricing and integration time.

**Routing**

| Adapter   | Weight |
| --------- | ------ |
| Sentiment | 0.40   |
| Summary   | 0.60   |

**Output**

> The client reacted positively to the demo but has concerns about cost and integration timeline, reflecting cautiously positive sentiment.

