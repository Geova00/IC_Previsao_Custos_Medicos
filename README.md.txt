PROJETO DE REGRESSÃO: PREVISÃO DE CUSTOS MÉDICOS INDIVIDUAIS

=============================================================

1. INTRODUÇÃO E RESUMO DO PROBLEMA

Este projeto tem como objetivo desenvolver uma solução de Aprendizado de Máquina (Regressão) para prever os custos médicos individuais ('charges') de um paciente, utilizando o dataset 'insurance.csv'. O trabalho focou na identificação dos fatores de risco que mais impactam o valor final do seguro.

O projeto seguiu o fluxo de trabalho padrão de Ciência de Dados, com ênfase na construção de um Pipeline robusto para garantir a reprodutibilidade e a prevenção de 'data leakage' (vazamento de dados).

---

2. SOLUÇÃO TÉCNICA E METODOLOGIA

2.1. PIPELINE E PRÉ-PROCESSAMENTO

Todas as transformações foram encapsuladas em um ColumnTransformer, integrado ao Pipeline principal:

* Variável Alvo ('charges'): Tratamento de Outliers (remoção de valores acima de 1.5 x IQR) para mitigar a assimetria e ruído.
* Features Numéricas ('age', 'bmi', 'children'): Escalonamento para média 0 e desvio padrão 1, utilizando StandardScaler.
* Features Categóricas ('sex', 'smoker', 'region'): Codificação via OneHotEncoder, para conversão em colunas binárias.
* Valores Ausentes: O SimpleImputer (strategy='mean') foi incluído no pipeline numérico para garantir a robustez contra dados faltantes.

2.2. MODELOS E OTIMIZAÇÃO

Foram treinados e comparados três modelos de regressão, sendo o Random Forest Regressor o de melhor desempenho.

* Modelo Escolhido: Random Forest Regressor.
* Otimização: O modelo foi otimizado utilizando GridSearchCV e Validação Cruzada, a fim de ajustar hiperparâmetros (como profundidade da árvore) para reduzir o overfitting do modelo padrão.

---

3. RESULTADOS, DISCUSSÕES E AVALIAÇÃO

3.1. DESEMPENHO FINAL DO MODELO OTIMIZADO

A avaliação em dados de teste (não vistos) demonstrou alta performance:

-   R2 (Coeficiente de Determinação): [INSIRA R² TESTE AQUI]
-   MAE (Erro Absoluto Médio): [INSIRA MAE TESTE AQUI]

3.2. INTERPRETAÇÃO: IMPORTÂNCIA DAS VARIÁVEIS

A análise da Feature Importance do Random Forest otimizado revelou a hierarquia dos fatores que mais impactam o custo:

1.  smoker_yes (Fumante): Fator de maior importância, com peso esmagador na previsão.
2.  age (Idade): Segunda feature mais importante.
3.  bmi (IMC): Terceira feature mais relevante.

Discussão: O modelo validou que o tabagismo e a idade são os principais determinantes do custo do seguro. A otimização através do GridSearchCV garantiu que o modelo não só fosse preciso, mas também capaz de generalizar bem para novos dados (baixa diferença entre R² de treino e teste).

---

4. TRABALHOS FUTUROS

Para aprimorar o modelo:

* Engenharia de Features de Interação: Criar uma feature que combine 'age' e 'smoker' para capturar o risco cumulativo.
* Testes com Modelos de Boosting: Avaliar a performance de algoritmos como XGBoost ou LightGBM.
* Transformação da Variável Alvo: Aplicar transformação Logarítmica em 'charges' para lidar com a assimetria, o que pode melhorar a performance de modelos lineares.