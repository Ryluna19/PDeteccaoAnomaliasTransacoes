# Detecção de Anomalias em Transações Financeiras

Projeto desenvolvido durante o curso de Inteligência Artificial Generativa do Bradesco.

O objetivo é analisar transações financeiras e comparar modelos de machine learning para identificar possíveis fraudes em um dataset fortemente desbalanceado.

> Apesar do nome da atividade mencionar “anomalias”, a abordagem utilizada é de classificação supervisionada, pois o dataset possui a coluna `Class`, que informa se uma transação é normal (`0`) ou fraudulenta (`1`).

---

## Objetivo

Analisar o impacto do desbalanceamento de classes na detecção de fraudes e comparar diferentes estratégias de classificação utilizando métricas como:

- Precision
- Recall
- F1-score
- Matriz de confusão
- ROC-AUC

---

## Dataset

O dataset contém transações financeiras classificadas como:

- `Class = 0`: transação normal
- `Class = 1`: transação fraudulenta

As colunas `V1` até `V28` são variáveis anonimizadas. Além delas, o dataset contém:

- `Time`: tempo da transação
- `Amount`: valor da transação
- `Class`: classificação da transação

O principal desafio do projeto é o forte desbalanceamento: fraudes representam uma parcela muito pequena das transações.

---

## Etapas realizadas

1. Carregamento e inspeção dos dados  
2. Análise do desbalanceamento das classes  
3. Preparação dos dados e transformação da variável `Amount`  
4. Separação entre treino e teste com estratificação  
5. Padronização de variáveis numéricas  
6. Regressão Logística como modelo baseline  
7. Ajuste do threshold de decisão  
8. Random Forest com `class_weight="balanced"`  
9. Balanceamento com SMOTE  
10. Random Forest treinado com dados balanceados  
11. XGBoost com `scale_pos_weight`  
12. Importância das variáveis  
13. Ajuste de hiperparâmetros com GridSearchCV  
14. Explicabilidade com SHAP  
15. Comparação final dos modelos  

---

## Modelos testados

- Regressão Logística com threshold padrão
- Regressão Logística com threshold ajustado para `0.30`
- Random Forest com balanceamento de classes
- Random Forest com SMOTE
- XGBoost com pesos para a classe minoritária
- XGBoost ajustado com GridSearchCV

---

## Principais conclusões

A análise mostrou que accuracy não é suficiente para avaliar modelos em dados desbalanceados.

A Regressão Logística serviu como baseline e mostrou que reduzir o threshold pode aumentar a quantidade de fraudes detectadas, mas também gera mais falsos positivos.

O Random Forest com `class_weight="balanced"` apresentou o melhor equilíbrio geral entre detecção de fraudes e quantidade de alertas incorretos.

Os modelos XGBoost detectaram mais fraudes, especialmente após o ajuste com GridSearchCV. Porém, esse ganho aumentou bastante a quantidade de falsos positivos.

Portanto, a escolha do modelo depende do equilíbrio desejado entre:

- reduzir fraudes não detectadas;
- evitar alertas falsos;
- capacidade operacional para revisar transações suspeitas.

---

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Imbalanced-learn
- XGBoost
- SHAP
- Jupyter Notebook

---

## Estrutura do projeto

```text
PDeteccaoAnomaliasTransacoes/
├── detecao_anomalias_transacoes.ipynb
├── comparacao_modelos.csv
├── requirements.txt
├── .gitignore
└── README.md