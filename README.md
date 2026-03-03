# 💳 Credit Card Fraud Detection using Machine Learning

## 📌 Executive Summary

Somos um banco digital com 2 milhões de clientes ativos.

Nos últimos 3 meses:

Volume mensal de transações: 35 milhões

Ticket médio: R$210

Taxa de fraude atual: 0,18%

Perda média por fraude confirmada: R$480

Prejuízo mensal estimado: ~R$30 milhões

Nosso modelo atual é antigo e gera muitos falsos positivos, bloqueando cartões legítimos e gerando insatisfação.

---

## 📊 Business Problem

Queremos desenvolver um modelo de detecção de fraude que:

Reduza perdas financeiras

Minimize bloqueios indevidos

Seja interpretável o suficiente para justificar decisões regulatórias

## 📦 Dataset

Source:  
https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

Dataset characteristics:

- 284,807 transactions
- 492 fraud cases (~0.17%)
- Highly imbalanced binary classification
- Features anonymized via PCA (V1–V28)
- Includes `Time`, `Amount`, and `Class` (target)

## 🛠️ Tecnologias Utilizadas
Python / Pandas (Manipulação de Dados)

XGBoost (Algoritmo Principal)

Scikit-Learn (Métricas e Preprocessamento)

Stratified K-Fold Cross-Validation (Validação Robusta)

RandomizedSearchCV (Otimização de Hiperparâmetros)

## ⚙️ Methodology

### 1️ Data Processing

- Data ingestion using PySpark
- Conversion to Pandas for modeling
- Missing value verification
- Class distribution analysis
- Stratified train/test split (80/20)

Stratification ensures fraud proportion consistency across datasets.

---

### 2️ Handling Class Imbalance

A abordagem escolhida foi o ajuste de Threshold 
Por padrão, o modelo classifica como "Fraude" tudo que tem probabilidade acima de 0.5. Em dados desbalanceados, você pode baixar esse limite para 0.2 ou 0.3 para capturar mais fraudes (aumentar o Recall).

### 3️ Model Comparison

Three models were evaluated:

#### 🔹 Logistic Regression
- Interpretable baseline model
- Class weighting to handle imbalance
- Fast and stable performance

#### 🔹 Random Forest
- Captures nonlinear patterns
- Robust to outliers
- Learns feature interactions

#### 🔹 LightGBM
- Gradient boosting framework
- Optimized for large-scale tabular data
- Efficient and production-oriented

The goal was not only performance comparison but understanding trade-offs between fraud detection and false alerts.

---

## 📊 Evaluation Strategy

Logistic Regression (Seu Baseline): É o modelo "desesperado". Ele tem um Recall altíssimo (91%), mas uma precisão pífia (6%). Ele detecta quase tudo, mas atira para todos os lados.

Random Forest: É o modelo "conservador". Tem uma Precisão absurda (96%), mas o menor Recall dos três (76%). Ele raramente erra um alarme, mas deixa passar 1 a cada 4 fraudes.

XGBoost: É o modelo "equilibrado". Ele tem o melhor AP (0.867). Ele consegue manter um Recall alto (86%) com uma Precisão aceitável (71%).

Vamos projetar o prejuízo em cima de 100 casos reais de fraude (para facilitar a conta proporcional):

Logistic Regression 8 perdidas (R$ 3.840)~1.400 falsos (R$ 28.000)R$ 31.840
Random Forest 24 perdidas (R$ 11.520)~3 falsos (R$ 60)R$ 11.580
XGBoost 13 perdidas (R$ 6.240)~35 falsos (R$ 700)R$ 6.940

 O XGBoost é o grande vencedor. Mesmo gerando um pouco mais de alarmes falsos que o Random Forest, a capacidade dele de evitar que a empresa perca R$ 480 em várias transações compensa muito o custo operacional.


## 🧠 Key Takeaways

. Eficiência Financeira (ROI)
Considerando uma perda média de R$ 480,00 por fraude e um custo operacional de R$ 20,00 por alarme falso (SAC/Logística):

Economia Gerada: O modelo evitou uma perda direta de R$ 42.240,00.

Custo Total do Erro: O prejuízo residual foi reduzido para R$ 5.550,00, o melhor desempenho entre todos os modelos testados.

2. Experiência do Cliente (Churn)
A taxa de falsos positivos foi controlada para evitar o bloqueio em massa. Com uma precisão de 63,8%, o modelo demonstra alta confiança, afetando apenas 0,08% da base de clientes legítimos. Isso minimiza a fricção no uso do cartão e reduz o abandono da plataforma.

3. Interpretabilidade e Governança
Através da análise de Feature Importance, o modelo identifica quais padrões comportamentais (variáveis V17, V14, V12) são críticos para a decisão. Isso permite que o time de risco audite as decisões do modelo e cumpra requisitos regulatórios de transparência em algoritmos financeiros.

## 🚀 How to Run

1. Install dependencies:



2. Run the notebook or script.

---

## 📁 Project Structure

---

## 👩‍💻 Author

Machine Learning applied with a business-impact orientation.
