# Life Expectancy - World Health Organization (WHO)

## 1. Dataset

Para este projeto, foi escolhido o dataset [Life Expectancy (WHO)](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who?select=Life+Expectancy+Data.csv), disponibilizado no Kaggle. A base reúne indicadores de saúde, educação e outros fatores relacionados á expectativa de vida de países classificados como `Developed` (desenvolvidos) ou `Developing` (em desenvolvimento), no período de 2000 a 2015

### Objetivo do projeto

O projeto tem como objetivo investigar se é possível prever se um país é classificado como desenvolvido ou em desenvolvimento utilizando somente indicadores de saúde e educação, sem utilizar o atributo `GDP` como identificador da classe.

**Tipo de problema:** Classificação.

**Dimensões iniciais do dataset:** 2.938 registros e 22 atributos.

## 2. Descrição dos atributos

A tabela abaixo apresenta os atributos do dataset e suas descrições.

<img width="1078" height="562" alt="image" src="https://github.com/user-attachments/assets/5f0f9605-5f9d-4590-9de6-b67033444531" />

## 3. Distribuição das classes

O atributo `Status` identifica cada registro como `Developed` (país desenvolvido) ou `Developing` (país em desenvolvimento).

A distribuição inicial das classes foi calculada considerando todos os registros do dataset:

<img width="295" height="166" alt="Captura de tela 2026-10-14 141351" src="https://github.com/user-attachments/assets/3fa1da31-3eaf-40c1-86a0-fa587610674b" />

**Observação:** os percentuais representam a proporção de registros de cada classe, e não a proporção de países únicos. Como a base contém observações referentes a vários anos, um mesmo país pode aparecer repetidamente.

### Cobertura temporal por país

A verificação da quantidade de observações por país identificou 193 países distintos, 183 que possuem 16 registros cada, correspondentes ao período de 2000 a 2015, e 10 países possuem apenas um registro.

<img width="335" height="70" alt="image" src="https://github.com/user-attachments/assets/298de951-f81d-4357-a1d4-f0b3810df86a" />

Para padronizar a análise somente no intervalo dos 16 anos, foi decidido manter apenas os países que possuem 16 registros. Essa decisão será aplicada na etapa de preparação dos dados e reduz a base para 183 países e 2.928 registros.

**Nota:** os resultados da distribuição das classes serão recalculados após a filtragem.

## 4. Valores faltantes

**Nota:** a análise foi realizada sobre os 2.938 registros e os 22 atributos da base, antes da remoção de países ou de qualquer tratamento dos dados.

Os valores faltantes estão concentrados principalmente nos atributos `Population` (652; 22,19%), `Hepatitis B` (553; 18,82%) e `GDP` (448; 15,25%). Por outro lado, atributos como por exemplo `Status`, `Country` e `Year` não apresentam valores faltantes.

<img width="316" height="447" alt="Captura de tela 2026-10-14 151409" src="https://github.com/user-attachments/assets/83e30f65-0160-4e4f-8c6f-f8d697524a7c" />

Também foi verificada a quantidade de registros que possuem pelo menos um valor faltante.

<img width="330" height="132" alt="image" src="https://github.com/user-attachments/assets/a4ce6c9e-014c-4308-9257-4557c8061858" />

Esses resultados indicam que o tratamento dos valores ausentes deve ser feito cuidadosamente para evitar a perda desnecessária de informações relevantes para o problema de classificação.
