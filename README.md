# 🎯 Telecom Churn Prediction: Inteligência Espacial vs. Modelagem Global

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Framework-orange.svg)](https://xgboost.readthedocs.io/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-blue)](https://scikit-learn.org/)

Este projeto aborda o clássico desafio de predição de cancelamento de clientes (Churn) em uma empresa de Telecomunicações através de uma perspectiva avançada de engenharia. Em vez de apenas aplicar um algoritmo genérico na base total, foi desenvolvido um ecossistema experimental comparando **Modelos Especialistas Regionalizados** (guiados por Redes Neurais de Kohonen e DBSCAN) contra um **Modelo Global Unificado**.

O objetivo principal foi encontrar o balanço ideal entre a **blindagem de faturamento** (capturar o máximo de Churn real - *Recall*) e a **eficiência de orçamento de retenção** (evitar acionar clientes estáveis - *Precisão*), mitigando os riscos de *Data Leakage* (vazamento de dados).

---

## 🔬 A Jornada de Arquitetura e Hipóteses

O projeto foi quebrado em três fases científicas para testar diferentes hipóteses de modelagem:

1. **Hipótese 1 (Segmentação Não-Linear):** Clientes em diferentes regiões do mapa comportamental possuem dores diferentes. Usamos **Self-Organizing Maps (SOM)** para projetar 36 variáveis e isolar a base em dois macro-perfiis: **Hemisfério Norte** (sensível a preço) e **Hemisfério Sul** (sensível a ofertas).
2. **Hipótese 2 (Micro-Engenharia de Recursos):** Dentro de cada hemisfério, aplicamos **DBSCAN** para agrupar clientes em "Ilhas de Serviço" de densidade semelhante. Criamos a feature autoral **`Island_Plus_Minus_Index`** (saldo de custo-benefício relativo do cliente frente aos seus vizinhos estatísticos). Treinamos dois modelos XGBoost especialistas.
3. **Hipótese 3 (Força Bruta e Volumetria - Navalha de Occam):** Confrontamos os especialistas contra um único **XGBoost Global Seco**, treinado na base original completa, sem viés de seleção e sem as features calculadas, avaliando se o volume bruto de dados superava a inteligência cirúrgica local.

---

## 📊 O Confronto Final: Placar Técnico Consolidado

A validação foi feita usando um **Split 70/30 Estratificado** em cima da massa de teste cega (**2.113 clientes** no modelo global). Para uma comparação justa, os resultados dos dois modelos especialistas (Norte + Sul) foram somados e contrastados com o modelo unificado:

| Métrica de Desempenho | Esteira de 2 Motores Especialistas<br>*(Norte + Sul)* | Modelo Global Seco<br>*(Vencedor de Produção)* | Impacto Líquido da Decisão |
| :--- | :---: | :---: | :---: |
| **Recall Ponderado** *(Taxa de Captura)* | 84.31% | **90.37%** | **+6.06% de Clientes Salvos** |
| **Erros Críticos** *(Deixou Escapar no Escuro)* | 88 clientes | **54 clientes** | **-34 Erros Críticos (Blindagem)** |
| **Precisão Ponderada** *(Foco do Orçamento)* | **60.71%** | 56.21% | -4.50% de Eficiência Comercial |
| **Alarmes Falsos** *(Gasto Inútil de Retenção)* | **306 alarmes** | 395 alarmes | +89 Disparos Errados |
| **Área Sob a Curva (ROC-AUC)** | 89.66% (Média) | **90.65%** | **+0.99% de Estabilidade** |

### 🧠 Decisão de Engenharia para Deploy
O **Modelo Global Seco foi o escolhido para ir para a Produção**. Pelo princípio da *Navalha de Occam*, ele entrega o maior retorno financeiro para o negócio ao reduzir os Erros Críticos para apenas 54 clientes perdidos, operando com uma arquitetura de código muito mais simples, sem o *overhead* computacional de calcular DBSCAN ou dicionários de médias em tempo real (redução drástica de débito técnico).

No entanto, **a clusterização por Kohonen reteve o valor estratégico do projeto**: enquanto o Modelo Global faz a predição fria de *quem* vai sair, a segmentação revelou ao time de marketing o *porquê* (Norte sangra por preço relativo e o Sul é vulnerável a contratos curtos com ofertas agressivas de entrada).

---

## 📁 Estrutura do Repositório

O projeto está organizado de forma limpa e estritamente profissional:

```text
├── data/
│   ├── raw/            # Dataset bruto original (telco.csv)
│   └── processed/      # Artefatos gerados (DataFrames persistidos e modelos .pkl)
├── notebooks/
│   ├── 01_analise_e_som.ipynb           # EDA, Redes de Kohonen e Raio-X de Hemisférios
│   ├── 02_laboratorios_avancados.ipynb  # Sub-clustering via DBSCAN, Plus-Minus e Modelos Locais
│   ├── 03_modelo_final_global.ipynb     # Tuning do Campeão de Produção e Exportação dos Artefatos
│   └── drafts/                          # Sandbox / Histórico de rascunhos locais de pesquisa
└── README.md                            # Documentação Principal do Portfólio