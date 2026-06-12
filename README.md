# Previsão de Churn Dinâmico e Retenção de Clientes em Telecomunicações

## 1. Contexto de Negócio e Impacto
No setor de telecomunicações, o custo para adquirir um novo cliente (CAC - Custo de Aquisição de Cliente) é significativamente maior do que o custo para reter um cliente atual. A perda de clientes (*Churn*) impacta diretamente a receita recorrente da empresa. Identificar clientes em risco de cancelamento antes que ele ocorra permite que a equipe de marketing e retenção atue de forma preventiva com ofertas personalizadas.

## 2. Objetivo do Projeto
Desenvolver um pipeline de dados e um modelo preditivo de classificação binária utilizando o ecossistema Python para estimar a probabilidade de um cliente ativo efetuar o cancelamento (*Churn*) no próximo mês, com base em seu histórico de consumo, perfil de contrato e dados demográficos.

## 3. Abordagem Analítica e Tecnologias
Este projeto aborda o ciclo completo de um problema de Ciência de Dados:
* **Análise Exploratória (EDA):** Identificação de anomalias, tratamento de dados faltantes ocultos e análise estatística das correlações de mercado.
* **Engenharia de Features:** Codificação de variáveis categóricas e normalização de variáveis numéricas.
* **Modelagem Preditiva:** Treinamento e ajuste de hiperparâmetros de modelos de classificação (ex: Regressão Logística, Random Forest e XGBoost).
* **Avaliação de Performance:** Otimização do modelo focando na métrica de **Recall** (Minimização de Falsos Negativos), garantindo que o negócio identifique o maior número possível de clientes em risco real.

**Tecnologias Utilizadas:** Python, Pandas, NumPy, SciPy, Scikit-Learn, Matplotlib, Seaborn.

## 4. Estrutura do Repositório
* `data/`: Armazenamento local dos dados brutos.
* `notebooks/`: Experimentos iniciais e visualizações gráficas.
* `src/`: Código modularizado para processamento e treinamento em produção.

---
*Nota: Projeto em desenvolvimento como parte do Portfólio de Ciência de Dados & IA.*