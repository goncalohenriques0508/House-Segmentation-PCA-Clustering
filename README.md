# 🏠 House Segmentation using PCA & Clustering

## 📌 Descrição

Projeto desenvolvido no âmbito da unidade curricular de Métodos de Aprendizagem Não Supervisionada, tendo obtido a classificação final **19 valores**.

O objetivo foi segmentar imóveis com base nas suas características estruturais e dimensionais, utilizando técnicas de redução de dimensionalidade (PCA) e métodos de clustering, de forma a compreender os fatores que influenciam o preço no mercado imobiliário.

---

## 🎯 Objetivos

- Reduzir a dimensionalidade do dataset através de PCA.
- Identificar dimensões latentes associadas às características das habitações.
- Aplicar diferentes métodos de clustering.
- Comparar qualidade dos clusters com métricas apropriadas.
- Analisar o impacto do ano de construção e renovação no preço final.

---

## 📊 Dataset

- ~4.600 registos iniciais
- 49 variáveis
- 4.099 observações finais após tratamento e remoção de outliers
- Variáveis estruturais, dimensionais e temporais (preço, ano construção, renovação)

---

## 🧹 Data Preparation

- Tratamento de valores inconsistentes
- Conversão e interpretação de variáveis fracionárias (nrWC, nrAndares)
- Remoção de outliers:
  - Preço < 2.5M
  - Sala_estar < 180m²
  - Lote < 20.000m²
  - Piso < 500m²
- Estandardização das variáveis para aplicação de PCA

---

## 📉 PCA (Principal Component Analysis)

- Seleção de 9 variáveis de input
- Testes de adequabilidade:
  - Bartlett’s Test
  - KMO
- Critérios de seleção:
  - Kaiser
  - Variância explicada (>60%)
- Extração de 3 Componentes Principais
- Rotação Varimax para interpretação

### Componentes Identificados

- **RC1** → Dimensão interna
- **RC2** → Estrutura e qualidade física
- **RC3** → Dimensão externa (tamanho do lote)

---

## 🔍 Clustering

### Métodos aplicados

- Clustering Hierárquico (Ward)
- K-Means
- Gaussian Mixture Model (GMM)

### Métricas utilizadas

- Silhouette Score
- WCSS
- BIC (para GMM)

---

## 🏘 Interpretação dos Clusters

Foram identificados 5 segmentos principais:

1. Casas clássicas de médio padrão
2. Casas modernas de alto padrão
3. Casas tradicionais de baixo padrão
4. Casas modernas de médio padrão
5. Casas de luxo / residências rurais

A segmentação revelou que:

- Casas pós-1980 com renovação significativa apresentam preços mais elevados.
- O tamanho do lote influencia fortemente o valor em segmentos de luxo.
- Renovação e ano de construção têm impacto direto na valorização do imóvel.

---

## 🛠 Tecnologias Utilizadas

- R
- PCA
- Clustering Hierárquico
- K-Means
- Gaussian Mixture Models
- Análise Estatística Multivariada

---

## 🧠 Competências Demonstradas

- Aplicação de técnicas de redução de dimensionalidade
- Avaliação de adequabilidade de PCA (KMO, Bartlett)
- Implementação de múltiplos métodos de clustering
- Comparação de métricas de qualidade de clusters
- Interpretação económica e de mercado
- Análise estatística multivariada
- Tratamento rigoroso de outliers
