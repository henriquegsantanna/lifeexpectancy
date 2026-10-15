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

## 3. Preparação dos Dados (Data Preparation)

### 3.1 Seleção das Variáveis

Para a modelagem, foram selecionados 14 indicadores relacionados à saúde e ao bem-estar:

- `Life expectancy`
- `Adult Mortality`
- `infant deaths`
- `Alcohol`
- `Hepatitis B`
- `Measles`
- `BMI`
- `under-five deaths`
- `Polio`
- `Total expenditure`
- `Diphtheria`
- `HIV/AIDS`
- `thinness 1-19 years`
- `thinness 5-9 years`

A variável `Status` foi definida como alvo da previsão. As colunas `Country`, `Year`, `GDP`, `Population`, `Schooling` e outras variáveis não selecionadas foram excluídas do conjunto de preditores.

### 3.2 Tratamento dos Valores Ausentes

Os valores ausentes das variáveis preditoras foram tratados por meio da imputação pela mediana de cada coluna.

Inicialmente, os dados foram divididos em conjuntos de treino e teste. Em seguida, as medianas foram calculadas exclusivamente a partir do conjunto de treino e aplicadas também ao conjunto de teste.

Esse procedimento foi adotado para evitar vazamento de informação (*data leakage*), garantindo que as informações do conjunto de teste não fossem utilizadas no ajuste do tratamento dos dados.

### 3.3 Divisão dos Dados

A base foi dividida em dois conjuntos:

- **Treino:** 2.342 registros, aproximadamente 80% dos dados.
- **Teste:** 586 registros, aproximadamente 20% dos dados.

Foi utilizada amostragem estratificada (*stratified split*) para preservar aproximadamente a proporção das classes nos dois conjuntos.

Após o tratamento, os conjuntos de treino e teste não apresentaram valores ausentes e estavam preparados para a etapa de modelagem.

## 4. Modelagem (Modeling)

### 4.1 Modelo 1 — Árvore de Decisão (Decision Tree)

O primeiro modelo implementado foi uma Árvore de Decisão, utilizando o algoritmo `DecisionTreeClassifier` da biblioteca Scikit-learn. Foi utilizado o parâmetro `class_weight='balanced'` para atribuir pesos às classes de acordo com suas frequências no conjunto de treino, considerando o desequilíbrio presente nos dados.

O modelo foi treinado com 2.336 registros e avaliado com 592 registros de teste, mantendo países distintos entre os dois conjuntos.

Os resultados obtidos foram:

- **Acurácia:** 92,23%.
- **Precisão da classe Developed:** 0,86.
- **Revocação da classe Developed:** 0,77.
- **F1-score da classe Developed:** 0,81.
- **Precisão da classe Developing:** 0,94.
- **Revocação da classe Developing:** 0,97.
- **F1-score da classe Developing:** 0,95.

A matriz de confusão apresentou 98 países desenvolvidos classificados corretamente, 30 classificados incorretamente como em desenvolvimento, 448 países em desenvolvimento classificados corretamente e 16 classificados incorretamente como desenvolvidos.

Os resultados indicam que o modelo apresentou bom desempenho geral, especialmente na identificação de países em desenvolvimento. Entretanto, a revocação da classe `Developed` foi inferior à da classe `Developing`, demonstrando que ainda existem dificuldades na identificação da classe minoritária.

### 4.2 Modelo 2 — Floresta Aleatória (Random Forest)

O segundo modelo implementado foi uma Floresta Aleatória, utilizando o algoritmo `RandomForestClassifier` da biblioteca Scikit-learn. Foram utilizadas 200 árvores de decisão, com o parâmetro `class_weight='balanced'` para considerar o desequilíbrio entre as classes.

O modelo foi treinado com 2.336 registros e avaliado com 592 registros de teste, mantendo a mesma divisão utilizada no primeiro experimento.

Os resultados obtidos foram:

- **Acurácia:** 88,85%.
- **Precisão da classe Developed:** 0,83.
- **Revocação da classe Developed:** 0,61.
- **F1-score da classe Developed:** 0,70.
- **Precisão da classe Developing:** 0,90.
- **Revocação da classe Developing:** 0,97.
- **F1-score da classe Developing:** 0,93.

Em comparação com a Árvore de Decisão, a Floresta Aleatória apresentou desempenho inferior nas métricas avaliadas, especialmente na revocação e no F1-score da classe `Developed`. Portanto, apesar de combinar várias árvores, esse modelo não apresentou melhores resultados neste experimento.

### 4.3 Importância dos Indicadores

Para compreender quais variáveis tiveram maior influência nas decisões do modelo, foi analisada a importância dos indicadores calculada pela Árvore de Decisão.

Os resultados mostraram que `Life expectancy` apresentou a maior importância, com aproximadamente 52,81%, seguido por `Alcohol`, com 22,03%. Em conjunto, esses dois indicadores representam aproximadamente 74,84% da importância total atribuída pelo modelo.

Outros indicadores, como `thinness 1-19 years` (6,78%), `Total expenditure` (3,44%) e `Hepatitis B` (3,37%), apresentaram contribuições menores.

Por outro lado, variáveis como `infant deaths` (0,17%) e `HIV/AIDS` (0,18%) apresentaram as menores importâncias no modelo.

Esses resultados indicam que a Árvore de Decisão utilizou principalmente a expectativa de vida e o indicador relacionado ao consumo de álcool para realizar suas classificações. Entretanto, a importância das variáveis representa sua contribuição para as decisões do modelo, não demonstrando necessariamente uma relação causal com o status de desenvolvimento dos países.

## 5. Avaliação (Evaluation)

### 5.1 Comparação dos Modelos

Foram avaliados dois algoritmos de classificação: Árvore de Decisão (*Decision Tree*) e Floresta Aleatória (*Random Forest*). Ambos foram treinados e avaliados utilizando os mesmos conjuntos de treino e teste, e os resultados obtidos foram:

**Decision Tree:**
![alt text](<Captura de tela 2026-10-15 134924.png>)

**Random Forest:**
![alt text](<Captura de tela 2026-10-15 135002.png>)

A Árvore de Decisão apresentou os melhores resultados nas métricas comparadas, alcançando acurácia de 92,23% e F1-score de 0,81 para a classe `Developed`. A Floresta Aleatória obteve acurácia de 88,85% e F1-score de 0,70 para essa mesma classe.

Embora ambos os modelos tenham apresentado bom desempenho na identificação de países em desenvolvimento, a Árvore de Decisão demonstrou maior capacidade de identificar corretamente os países classificados como desenvolvidos.

### 5.2 Análise dos Erros de Classificação

A matriz de confusão da Árvore de Decisão apresentou os seguintes resultados:

- 98 países desenvolvidos foram classificados corretamente.
- 30 países desenvolvidos foram classificados incorretamente como em desenvolvimento.
- 448 países em desenvolvimento foram classificados corretamente.
- 16 países em desenvolvimento foram classificados incorretamente como desenvolvidos.

Esses resultados demonstram que, apesar do bom desempenho geral, o modelo ainda apresenta dificuldades na identificação de parte dos países desenvolvidos.

### 5.3 Seleção do Modelo

Com base nos resultados obtidos, a Árvore de Decisão foi selecionada como o melhor modelo entre os dois algoritmos testados.

A escolha foi baseada na maior acurácia e no melhor desempenho de F1-score e recall para a classe `Developed`, que representa a categoria minoritária do dataset.
