# 🏠 House Segmentation — PCA & Clustering

![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)
![PCA](https://img.shields.io/badge/PCA-Dimensionality%20Reduction-blue?style=flat)
![Clustering](https://img.shields.io/badge/Clustering-K--Means%20%7C%20Hierarchical%20%7C%20GMM-orange?style=flat)
![Grade](https://img.shields.io/badge/Grade-19%2F20-brightgreen?style=flat)

Unsupervised learning project segmenting real estate properties using **PCA** for dimensionality reduction and three clustering methods (**Hierarchical**, **K-Means**, **GMM**) to uncover market segments and analyse the impact of construction year and renovation on property prices.

---

## 📌 Descrição

Projeto desenvolvido no âmbito da unidade curricular de Métodos de Aprendizagem Não Supervisionada, tendo obtido a classificação final **19 valores**.

O objetivo foi segmentar imóveis com base nas suas características estruturais e dimensionais, utilizando técnicas de redução de dimensionalidade (PCA) e métodos de clustering, de forma a compreender os fatores que influenciam o preço no mercado imobiliário.

---

## 📊 Dataset

- Ficheiro: `Preco_casas_final.xlsx` (Sheet2)
- ~4.600 registos no dataset completo (partilhado entre grupos de trabalho)
- Cada grupo filtra os seus registos através de colunas de atribuição (`T2Gr04 == 1`)
- 12 variáveis utilizadas: `preco`, `nrQuartos`, `nrWC`, `Sala_estar_m2`, `lote_m2`, `nrAndares`, `vista`, `condicao`, `piso_m2`, `arrecadacao_m2`, `Ano_construcao`, `Ano_renovacao`

---

## 🧹 Data Preparation

- Correção de variáveis com valores decimais inapropriados:
  - `nrWC` (casas de banho em frações de 0.25)
  - `nrAndares` (andares em frações de 0.5)
- Correção de registos com `Ano_renovacao` < `Ano_construcao` → definido como 0
- Remoção de outliers:
  - `preco` < 2.5M
  - `Sala_estar_m2` < 180m²
  - `lote_m2` < 20.000m²
  - `piso_m2` < 500m²
  - `arrecadacao_m2` < 750m²
- Resultado final: 4.099 observações

---

## 📉 PCA (Principal Component Analysis)

- **Input**: 9 variáveis estruturais e dimensionais (`preco`, `Ano_construcao` e `Ano_renovacao` excluídas — usadas apenas na interpretação dos clusters)
- Testes de adequabilidade: Bartlett's Test + KMO
- Critérios de seleção de componentes: Kaiser + variância explicada (>60%)
- Extração de **3 Componentes Principais** com rotação Varimax

### Componentes Identificados

| Componente | Nome | Variáveis dominantes |
|---|---|---|
| RC1 | Dimensão interna | `Sala_estar_m2`, `piso_m2`, `nrQuartos`, `nrWC` |
| RC2 | Altura | `nrAndares`, `condicao`, `vista` |
| RC3 | Dimensão externa | `lote_m2`, `arrecadacao_m2` |

---

## 🔍 Clustering

Os clusters foram construídos sobre os scores dos 3 componentes principais.

| Método | Configuração | Métrica |
|---|---|---|
| Hierárquico (Ward.D2) | Corte em h=35 → 5 clusters | Silhouette |
| K-Means | 5 clusters | WCSS + Silhouette |
| GMM (mclust) | Seleção automática via BIC | BIC |

O cluster final atribuído a cada observação é o do **K-Means**.

---

## 🏘 Interpretação dos Clusters

Os 5 segmentos foram interpretados cruzando os scores dos componentes com `preco`, `Ano_construcao` e `Ano_renovacao`:

1. Casas clássicas de médio padrão
2. Casas modernas de alto padrão
3. Casas tradicionais de baixo padrão
4. Casas modernas de médio padrão
5. Casas de luxo / residências rurais

Principais conclusões:

- Casas pós-1980 com renovação significativa apresentam preços mais elevados.
- O tamanho do lote influencia fortemente o valor em segmentos de luxo.
- Renovação e ano de construção têm impacto direto na valorização do imóvel.

---

## 🛠 Tecnologias Utilizadas

- R (`psych`, `cluster`, `mclust`, `corrplot`, `dplyr`)
- PCA com rotação Varimax
- Clustering Hierárquico (Ward.D2)
- K-Means
- Gaussian Mixture Models (mclust)
