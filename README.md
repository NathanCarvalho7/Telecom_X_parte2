# 🤖 Previsão de Evasão de Clientes (Churn) — Telecom X parte 2

---

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-yellow)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Boosting-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Data%20Viz-brightgreen)

---

## 📌 Descrição do Projeto

Este projeto dá continuidade à análise da **evasão de clientes (Churn)** da empresa fictícia **Telecom X**.

Após a fase de **análise exploratória de dados (EDA)**, o objetivo agora é construir **modelos preditivos de Machine Learning** capazes de **prever quais clientes têm maior probabilidade de cancelar o serviço**.

A partir dos dados tratados e das variáveis mais relevantes identificadas na parte 1, foram treinados e avaliados diferentes algoritmos para **comparar seu desempenho e extrair os principais fatores que influenciam o churn**.

---

# 🎯 Objetivo

Construir e avaliar modelos preditivos para responder à pergunta:

> É possível prever, com base em dados históricos, quais clientes estão propensos a cancelar o serviço?

Além disso, busca-se **identificar as variáveis mais importantes** para o cancelamento, permitindo ações de retenção mais direcionadas.

---

# 📊 O que foi analisado?

Nesta etapa, foram utilizadas todas as variáveis preparadas na fase anterior, incluindo:

* 📅 Tempo de contrato
* 💰 Valores de cobrança (mensal e total)
* 💳 Método de pagamento
* 🌐 Tipo de serviço de internet
* 🛡️ Serviços adicionais (segurança, suporte, backup)
* 📺 Serviços de streaming
* 📑 Tipo de contrato

Essas variáveis foram transformadas (via one‑hot encoding) e utilizadas para alimentar os modelos preditivos.

---

# 🛠️ Tecnologias Utilizadas

* Python
* Pandas / NumPy
* Scikit‑learn (Regressão Logística, Random Forest, métricas)
* XGBoost
* Matplotlib / Seaborn
* Google Colab

---

# 📈 Etapas da Modelagem

## 1️⃣ Preparação dos Dados

* Carregamento do arquivo tratado na parte 1
* Remoção de colunas irrelevantes (`id_cliente`, `faixa_tempo`)
* **One‑hot encoding** das variáveis categóricas
* Verificação da proporção de evasão (**26,6%** de cancelamentos)
* **Normalização** dos dados (apenas para a Regressão Logística, via `StandardScaler`)

---

## 2️⃣ Análise de Correlação e Seleção de Variáveis

* Matriz de correlação com a variável alvo (`cancelou`)
* Identificação das **variáveis mais correlacionadas**:
  * Positivas: `tipo_contrato_Mensal`, `seguranca_online_Não`, `suporte_tecnico_Não`
  * Negativas: `meses_contrato`, `tipo_contrato_2 anos`
* Análises direcionadas com **boxplots e gráficos de barras** para confirmar padrões.

---

## 3️⃣ Modelagem Preditiva

Foram treinados **dois modelos** com abordagens diferentes:

| Modelo                | Característica                          | Exige normalização? |
|-----------------------|-----------------------------------------|---------------------|
| Regressão Logística   | Linear, interpretável                   | ✅ Sim              |
| Random Forest         | Ensemble, não linear, robusto           | ❌ Não              |

* **Separação treino‑teste:** 70% / 30% com estratificação
* **Métricas avaliadas:** Acurácia, Precisão, Recall, F1‑score e Matriz de Confusão

---

## 4️⃣ Resultados

| Modelo               | Acurácia | Precisão | Recall | F1‑score |
|----------------------|----------|----------|--------|----------|
| Regressão Logística  | 0,8024   | 0,6552   | 0,5419 | 0,5932   |
| Random Forest        | 0,7825   | 0,6197   | 0,4706 | 0,5350   |

* A **Regressão Logística** apresentou melhor desempenho geral, especialmente no **recall** (capacidade de identificar quem realmente cancela).
* O **Random Forest** apresentou **overfitting**: 99,8% de acurácia no treino contra 78,2% no teste.

---

## 5️⃣ Importância das Variáveis

**Random Forest – Top 5 fatores mais importantes:**

1. `cobranca_total` (total gasto pelo cliente)
2. `meses_contrato` (tempo de casa)
3. `conta_diaria` (gasto médio diário)
4. `cobranca_mensal` (valor da fatura mensal)
5. `tipo_contrato_Mensal` (contrato mês a mês)

**Regressão Logística – coeficientes mais influentes:**

* **Aumentam a chance de evasão:** `cobranca_total`, `servico_internet_Fibra ótica`, `tipo_contrato_Mensal`, `metodo_pagamento_Cheque eletrônico`, `suporte_tecnico_Não`.
* **Reduzem a chance de evasão:** `meses_contrato`, `tipo_contrato_2 anos`, `servico_internet_DSL`.

---

# 🧠 Principais Insights

* Clientes com **contrato mensal** e **cheque eletrônico** como forma de pagamento estão entre os perfis de **maior risco**.
* A **ausência de suporte técnico** e outros serviços adicionais também está fortemente associada ao churn.
* Quanto **maior o tempo de contrato** e o **total gasto acumulado**, **menor a probabilidade de cancelamento** (clientes antigos e engajados).
* Os modelos mostram que é possível **prever churn com boa assertividade**, especialmente utilizando **Regressão Logística**, que também oferece alta interpretabilidade.

---

# 💡 Recomendações de Negócio

1. **Foco em contratos longos:** incentivar planos anuais ou bienais com benefícios.
2. **Estimular métodos de pagamento automáticos** (cartão de crédito, débito automático).
3. **Oferecer serviços de suporte e segurança** como parte de pacotes promocionais para clientes em risco.
4. **Monitorar clientes nos primeiros meses** com ações de engajamento e pesquisas de satisfação.
5. **Revisar a oferta de fibra óptica e streaming** se esses serviços estiverem gerando insatisfação ou custo elevado para o cliente.

---

# 🚀 Possíveis Melhorias Futuras

* Aplicar técnicas de **balanceamento de classes (SMOTE)** para melhorar o recall.
* **Ajustar hiperparâmetros** do Random Forest para reduzir overfitting.
* Testar outros modelos, como **XGBoost** ou **Redes Neurais**.
* Criar um **dashboard interativo** para visualizar as previsões em tempo real.
* Implementar um **sistema de alerta** para clientes com alta probabilidade de churn.

---

# 📁 Estrutura do Projeto

```
📂 telecom-churn-prediction
 ├── Telecom_X_parte_2.ipynb
 ├── README.md
 ├── dados_tratados.csv
```

---

# 👤 Autor

| [<img src="https://github.com/NathanCarvalho7.png" width=115><br><sub>Nathan Carvalho</sub>](https://github.com/NathanCarvalho7) |
| :------------------------------------------------------------------------------------------------------------------------------: |

Projeto desenvolvido para prática de **Machine Learning aplicado à predição de churn**, utilizando dados simulados de uma empresa de telecomunicações.
