# Bayesian Network Interface Documentation

## Model Overview
This Bayesian Network predicts heart disease (`target`) based on patient demographics and medical test results. The network structure is:
age → fbs → target → chol
↓
thalach

text

## Model Components

### 1. Variables and Discretization
| Variable  | Type      | Bins/Range                          | Description                     |
|-----------|-----------|-------------------------------------|---------------------------------|
| age       | Discrete  | young(<40), middle(40-60), old(>60) | Patient age                     |
| fbs       | Binary    | 0, 1                                | Fasting blood sugar > 120 mg/dL |
| target    | Binary    | 0, 1                                | Heart disease presence          |
| chol      | Discrete  | normal(<200), borderline(200-239), high(≥240) | Serum cholesterol (mg/dL) |
| thalach   | Discrete  | low(<100), medium(100-140), high(>140) | Maximum heart rate achieved |

### 2. Conditional Probability Distributions (CPDs)

#### Age Distribution
```python
+-------------+-----------+
| age(middle) | 0.6788    |
| age(old)    | 0.2616    |
| age(young)  | 0.0596    |
+-------------+-----------+
```
FBS Given Age
```
python
+--------+---------------------+---------------------+------------+
| age    | middle              | old                 | young      |
+--------+---------------------+---------------------+------------+
| fbs(0) | 0.8439              | 0.8354              | 1.0        |
| fbs(1) | 0.1561              | 0.1646              | 0.0        |
+--------+---------------------+---------------------+------------+
```
Target Given FBS
```
python
+-----------+---------------------+--------------------+
| fbs       | fbs(0)              | fbs(1)             |
+-----------+---------------------+--------------------+
| target(0) | 0.4514              | 0.4889             |
| target(1) | 0.5486              | 0.5111             |
+-----------+---------------------+--------------------+
```
Cholesterol Given Target
```
python
+-----------------------+---------------------+---------------------+
| target                | target(0)           | target(1)           |
+-----------------------+---------------------+---------------------+
| chol(borderline_high) | 0.2754              | 0.3598              |
| chol(high)            | 0.5725              | 0.4634              |
| chol(normal)          | 0.1522              | 0.1768              |
+-----------------------+---------------------+---------------------+
```
Thalach Given Target
```
python
+-----------------+----------------------+----------------------+
| target          | target(0)            | target(1)            |
+-----------------+----------------------+----------------------+
| thalach(high)   | 0.5290               | 0.8415               |
| thalach(low)    | 0.0507               | 0.0061               |
| thalach(medium) | 0.4203               | 0.1524               |
+-----------------+----------------------+----------------------+
```
Inference Examples
Example 1: High-Risk Patient
```
python
evidence = {'age': 'old', 'fbs': 1, 'chol': 'high', 'thalach': 'high'}
result = inference.query(variables=['target'], evidence=evidence)
```
Result:
```
text
+-----------+---------------+
| target(0) |        0.4262 |
| target(1) |        0.5738 |
+-----------+---------------+
```
Interpretation: 57.4% probability of heart disease

Example 2: Low-Risk Patient
```
python
evidence = {'age': 'middle', 'fbs': 0, 'chol': 'normal', 'thalach': 'medium'}
result = inference.query(variables=['target'], evidence=evidence)
```
Result:
```
text
+-----------+---------------+
| target(0) |        0.6612 |
| target(1) |        0.3388 |
+-----------+---------------+
```
Interpretation: 33.9% probability of heart disease

Usage Guide
Load the trained model:
```
python
from pgmpy.inference import VariableElimination
inference = VariableElimination(model)
```
Make predictions:
```
python
evidence = {
    'age': 'middle',    # young/middle/old
    'fbs': 0,           # 0 or 1
    'chol': 'normal',   # normal/borderline_high/high
    'thalach': 'medium' # low/medium/high
}
result = inference.query(variables=['target'], evidence=evidence)
```
Key Insights
Older patients with high heart rates have >50% heart disease risk

Normal cholesterol and medium heart rate indicate lower risk (~34%)

Fasting blood sugar has modest impact on predictions

High heart rate is strongly associated with heart disease
