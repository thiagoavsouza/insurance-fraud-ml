# Detecção de Fraude em Seguro -- Comparação de Modelos de Machine Learning

## Descrição do Projeto

Este repositório reúne **cinco projetos de modelagem preditiva**
aplicados à detecção de **fraude em sinistros de seguro**.\
Cada projeto utiliza um algoritmo diferente, permitindo avaliar ganhos
de performance, robustez e interpretabilidade ao longo da evolução das
técnicas.

Os modelos desenvolvidos, em ordem cronológica, foram:

1.  **Regressão Logística**\
2.  **Decision Tree**\
3.  **Random Forest**\
4.  **XGBoost**\
5.  **LightGBM**

O foco está em analisar desempenho em um cenário **altamente
desbalanceado**, escolher o cutoff mais adequado e traduzir resultados
em ações operacionais.

------------------------------------------------------------------------

## Objetivos

-   Realizar análise exploratória do conjunto de dados\
-   Pré-processar features e preparar o dataset para modelagem\
-   Aplicar cinco técnicas de classificação\
-   Comparar performance entre os modelos\
-   Avaliar cutoff ótimo / thresholds ajustados\
-   Interpretar impacto operacional (FP, FN, recall, precisão)\
-   Fornecer recomendações práticas de uso em sinistros e prevenção a
    fraude

------------------------------------------------------------------------

## Etapas Gerais dos Projetos

1.  **Importação e inspeção dos dados** --- formato, datatypes, missing
    values, proporção de fraude\
2.  **Pré-processamento** --- limpeza, codificação, padronização quando
    necessário\
3.  **Treinamento dos modelos** --- sklearn, XGBoost, LightGBM\
4.  **Avaliação de desempenho** --- AUC, matriz de confusão, recall,
    precision\
5.  **Ajuste de Cutoff** --- Youden, maximização de recall, ou
    balanceamento conforme objetivo\
6.  **Comparação técnica entre modelos**\
7.  **Conclusão e pontos para evolução futura**

------------------------------------------------------------------------

## Comparação dos Modelos (Resumo)

  ------------------------------------------------------------------------------
  Modelo                  Características   Pontos Fortes    Limitações
  ----------------------- ----------------- ---------------- -------------------
  **Regressão Logística** Baseline          Coeficientes     Não captura
                          interpretável     claros; rápido   relações complexas

  **Decision Tree**       Modelo não linear Interpretação    Pode sofrer
                                            visual           overfitting

  **Random Forest**       Ensemble de       Robusto; boa     Treino mais lento
                          árvores           performance      

  **XGBoost**             Boosting          Alta             Mais complexo para
                          otimizado         performance;     tunar
                                            controle de      
                                            overfitting      

  **LightGBM**            Boosting rápido   Excelente em     Exige cuidado no
                                            grandes volumes  pré-processamento
  ------------------------------------------------------------------------------

------------------------------------------------------------------------

## Resultados Principais (exemplo ilustrativo)

-   **AUC Geral dos Modelos:** entre 0.84 e 0.96\
-   **Modelos de melhor performance:** Random Forest, LightGBM e
    XGBoost\
-   **Modelos mais interpretáveis:** Regressão Logística e Decision
    Tree\
-   **Recall otimizado via cutoff** nos modelos ensemble mostrou melhor
    capacidade de identificar fraudes\
-   **Trade-off natural:** maior recall → mais falsos positivos
    (esperado em prevenção a fraude)

> Em todos os modelos, buscou-se priorizar **sensibilidade**, já que o
> custo de não detectar uma fraude é muito superior ao custo de
> investigar um falso positivo.

------------------------------------------------------------------------

## Recomendações Operacionais

-   Priorizar investigação dos **N% maiores scores** conforme capacidade
    operacional\
-   Monitorar **precision** e **taxa de falsos positivos**
    periodicamente\
-   Recalibrar o cutoff a cada novo período (mensal/trimestral)\
-   Considerar **XGBoost, LightGBM ou Random Forest** em ambiente de
    produção\
-   Criar dashboards para acompanhar métricas como:
    -   AUC\
    -   Recall por faixas\
    -   Volume de alertas\
    -   Falsos positivos por cluster de clientes

------------------------------------------------------------------------

## Principais Bibliotecas Utilizadas

``` bash
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
lightgbm
statsmodels
imblearn
```

------------------------------------------------------------------------

## Como Executar os Projetos

1.  Instalar dependências:

``` bash
pip install -r requirements.txt
```

2.  Abrir o notebook de cada modelo na pasta `/notebooks/`\
3.  Executar as células sequencialmente: pré-processamento → modelagem →
    avaliação\
4.  Ajustar o cutoff conforme objetivo operacional do time de fraude

------------------------------------------------------------------------

## Contato

E-mail: **thiago.a.v.souza@gmail.com**\
LinkedIn: **https://www.linkedin.com/in/thiagoavsouza/**
