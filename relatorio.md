# Relatório do Projeto — Life Expectancy (WHO)

## 1. Entendimento do Negócio (Business Understanding)

### 1.1 Definição do Problema

O projeto tem como objetivo investigar se indicadores relacionados à saúde e ao bem-estar podem ser utilizados para classificar países de acordo com seu status de desenvolvimento.

Para isso, será utilizado o dataset *Life Expectancy (WHO)*, que reúne informações sobre expectativa de vida e outros indicadores de saúde de diferentes países de 2000 a 2015.

O problema será tratado como classificação binária, na qual o modelo deverá prever se um país pertence à categoria `Developed` (desenvolvido) ou `Developing` (em desenvolvimento), com base nos indicadores relacionados a ODS 3 — Saúde e Bem-Estar.

### 1.2 Objetivo do Projeto

O objetivo é desenvolver e avaliar modelos de Machine Learning capazes de classificar o status de desenvolvimento dos países a partir de indicadores relacionados à ODS 3.

Além da classificação, pretende-se identificar quais indicadores apresentam maior relevância para as previsões realizadas pelos modelos.

### 1.3 Escopo

O projeto compreende a análise exploratória dos dados, a preparação do dataset, o treinamento de modelos de classificação e a avaliação de seus resultados.

A análise será realizada em Python, utilizando o Google Colab, com bibliotecas de análise de dados e Machine Learning.

### 1.4 Critérios de Avaliação

Os modelos serão avaliados utilizando métricas de classificação, incluindo acurácia (*accuracy*), precisão (*precision*), revocação (*recall*) e F1-score.

Como as classes apresentam proporções diferentes, a análise não será baseada exclusivamente na acurácia. Também será considerada a matriz de confusão, permitindo observar os acertos e erros de classificação em cada categoria.

## 2. Entendimento dos Dados (Data Understanding)

### 2.1 Origem dos Dados

O dataset utilizado é o *Life Expectancy (WHO)*, disponibilizado no Kaggle e associado a indicadores de saúde publicados pela OMS.

A base reúne informações de diferentes países entre os anos de 2000 e 2015, incluindo indicadores relacionados à expectativa de vida, mortalidade, vacinação, doenças e outros fatores associados à saúde.

Fonte: [Life Expectancy Data — Kaggle](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who)

### 2.2 Características do Dataset

Inicialmente, o dataset possuía 2.938 registros e 22 colunas, abrangendo informações de 193 países.

Após a filtragem, foram mantidos os países que possuíam 16 registros, correspondentes à quantidade esperada para o período de 2000 a 2015. Com isso, a base passou a conter 2.928 registros e 22 colunas.

A variável `Status` foi definida como variável-alvo, apresentando duas categorias: `Developed` e `Developing`.

Após a filtragem, a distribuição das classes ficou da seguinte forma:

- `Developing`: 2.416 registros (82,51%).
- `Developed`: 512 registros (17,49%).

Essa distribuição demonstra um desequilíbrio entre as classes, que deverá ser considerado durante a avaliação dos modelos.

### 2.3 Exploração e Qualidade dos Dados

Durante a análise inicial, foram identificados nomes de colunas com espaços excedentes, que foram padronizados para facilitar a manipulação dos dados.

Também foram analisados os valores ausentes e a existência de registros duplicados. Na base filtrada, foram identificadas 1.279 linhas com pelo menos um valor ausente e nenhum registro duplicado.

Entre as colunas com maior quantidade de valores ausentes, destacam-se `Population`, `Hepatitis B`, `GDP` e `Total expenditure`.

A descrição detalhada dos atributos, da distribuição das classes e dos valores ausentes encontra-se no arquivo `descdataset.md`.
