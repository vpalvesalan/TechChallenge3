# ✈️ Previsão de Atrasos de Voos (Flight Delay Prediction)

**Tech Challenge - Pós-graduação em Machine Learning** **Autor:** Alan Alves

## 📋 Sobre o Projeto

Este projeto tem como objetivo desenvolver uma solução de Machine Learning para prever atrasos de voos comerciais nos EUA. O foco principal é identificar, com **30 minutos de antecedência da chegada prevista**, se um voo atrasará 5 minutos ou mais (`IS_DELAYED_5MIN`).

A solução visa auxiliar na **gestão proativa de conexões** e alocação de recursos aeroportuários, priorizando a identificação correta dos atrasos (alto Recall) para minimizar perdas operacionais.

---

## 📂 Estrutura do Projeto (Notebooks)

O desenvolvimento foi dividido em 4 etapas principais. Abaixo você encontra o link para cada notebook e um resumo do seu conteúdo:

* **[1_EDA.ipynb](./1_EDA.ipynb)** **Limpeza e Preparação de Dados:** Foca na ingestão dos dados brutos, tratamento de valores nulos, conversão de tipos e criação do dataset base limpo (`df_limpo_com_features.parquet`).

* **[2_EDA_visuals.ipynb](./2_EDA_visuals.ipynb)** **Análise Exploratória e Baseline:** Aprofunda na análise visual das variáveis (sazonalidade, horários), engenharia de features (como taxas históricas de rotas) e estabelece um modelo **Baseline (Regressão Logística)** para comparação de performance.

* **[3_Modelo_Supervissionado.ipynb](./3_Modelo_Supervissionado.ipynb)** **Modelagem Preditiva Avançada:** Treinamento e avaliação de modelos de Gradient Boosting (**LightGBM** e **CatBoost**). Inclui a análise de *Feature Importance*, comparação de métricas (AUC, Recall, F1) e serialização dos modelos finais.
    * *Modelo Vencedor:* LightGBM (AUC ~0.94).

* **[4_Modelo_nao_supervisionado.ipynb](./4_Modelo_nao_supervisionado.ipynb)** **Clusterização de Aeroportos:** Aplicação de algoritmos não supervisionados (**K-Means** e **DBSCAN**) para segmentar aeroportos baseados em eficiência operacional (atrasos, tempo de táxi e volume), identificando *hubs* congestionados e anomalias operacionais.

---

## 🚀 Principais Resultados

### Modelagem Supervisionada (LightGBM)
O modelo final superou significativamente o baseline, oferecendo uma ferramenta útil para a operação:
* **AUC-ROC:** 0.9447 (Excelente capacidade de separação entre classes).
* **Recall (Classe Atraso):** 84% (Captura a grande maioria dos atrasos reais).
* **Fator Crítico:** O atraso na partida (`DEPARTURE_DELAY`) é o maior preditor, seguido pelo tempo de taxiamento (`TAXI_OUT`).

### Modelagem Não Supervisionada (Clusterização)
A análise de aeroportos revelou insights estruturais da malha aérea:
* **K-Means:** Identificou uma dicotomia clara entre "Mega Hubs" (alto volume, maior tempo de solo) e Aeroportos Regionais (menor volume, maior agilidade).
* **DBSCAN:** Detectou outliers críticos como **JFK** e **LGA** (Nova York), que possuem tempos de taxiamento quase o dobro da média nacional, representando gargalos logísticos severos.

---

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.12.2
* **Manipulação de Dados:** Pandas, Numpy
* **Visualização:** Matplotlib, Seaborn
* **Machine Learning:** Scikit-Learn, LightGBM, CatBoost
* **Formatos de Dados:** Parquet

---

## 📦 Como Executar

1.  Clone este repositório.
2.  Instale as dependências listadas nos notebooks (recomenda-se criar um ambiente virtual).
3.  Execute os notebooks na ordem numérica (1 a 4) para reproduzir o pipeline completo, garantindo que os arquivos `.parquet` gerados em uma etapa estejam disponíveis para a próxima.