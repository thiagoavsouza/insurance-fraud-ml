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


| Modelo                  | AUC         | Precision (fraude) | Recall (fraude) | F1 fraude  | Accuracy   | FP (ruído)       |
| ----------------------- | ----------- | ------------------ | --------------- | ---------- | ---------- | ---------------- |
| **Regressão Logística** | 0.806       | 0.13               | **0.94**        | 0.22       | 0.61       | altíssimo        |
| **Decision Tree**       | 0.824       | 0.13               | **0.96**        | 0.22       | 0.60       | altíssimo        |
| **Random Forest**       | 0.870       | 0.21               | 0.81            | 0.33       | 0.80       | alto             |
| **LightGBM**            | 0.936       | 0.51               | 0.68            | 0.58       | 0.94       | **médio**        |
| ⭐ **XGBoost**           | ⭐ **0.959** | ⭐ **0.64**         | 0.68            | ⭐ **0.66** | ⭐ **0.96** | ⭐ **mais baixo** |

------------------------------------------------------------------------

## Resultados Principais

![alt text](image.png)

-   **AUC Geral dos Modelos:** entre 0.81 e 0.96\
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

## Conclusão Geral

O **XGBoost é o modelo mais recomendado** para implantação operacional, pois maximiza a identificação de fraudes, reduz drasticamente falsos positivos e melhora significativamente a eficiência do time de sinistros.

A comparação entre Regressão Logística, Decision Tree, Random Forest, XGBoost e LightGBM revela um cenário consistente: **todos os modelos identificam padrões relevantes de fraude**, porém cada um entrega esse resultado com um equilíbrio diferente entre **efetividade (recall)** e custo **operacional (falsos positivos).**

Entre todas as abordagens, o **XGBoost** se destaca como a solução mais eficiente para aplicação prática na seguradora. Ele apresenta:

- **Melhor AUC (0.959)** entre os modelos testados

- **Alta capacidade de detecção (recall ≈ 68%)**

- **Baixíssimo volume de falsos positivos** em comparação com as demais técnicas

- **Melhor equilíbrio entre precisão, sensibilidade e esforço operacional**

Essa combinação indica que o modelo é tecnicamente superior e, ao mesmo tempo, viável para uso real, pois reduz drasticamente a quantidade de alertas falsos sem comprometer a capacidade de encontrar fraudes.

Modelos como **Random Forest e LightGBM** também apresentam boa performance, mas ainda geram um volume maior de falsos positivos ou um recall menor, impactando a produtividade do time de investigação.

Já a **Regressão Logística**, embora apresente recall muito elevado, cria um **volume inviável de falsos positivos**, o que tornaria o processo operacionalmente custoso, lento e difícil de escalar. Esse modelo é adequado como baseline, mas não como solução final.

------------------------------------------------------------------------

## Recomendações Operacionais

Para garantir que o modelo de detecção de fraude gere impacto real na rotina do time de Sinistros e mantenha desempenho ao longo do tempo, recomenda-se:

**1. Priorização baseada em risco**

- Investigar diariamente os N% maiores scores, de acordo com a capacidade operacional do time.

- Essa abordagem maximiza o volume de fraudes detectadas com menor esforço.

**2. Monitoramento contínuo de métricas-chave**

Acompanhar periodicamente:

- **Precision (classe fraudulenta)** – para controlar o volume de falsos positivos

- **Recall** – para garantir que o modelo continue encontrando fraudes
- **Taxa de falsos positivos** por cluster/perfil de cliente

- **AUC** (como medida global de separação)

**3. Recalibração do Cutoff**

Ajustar mensalmente ou trimestralmente o threshold, conforme:

- Mudanças no perfil das fraudes
- Sazonalidades
- Novos dados operacionais

Esse ajuste evita perda de Recall ou explosão de alertas desnecessários.

**4. Evolução e manutenção do modelo**

Avaliar o uso de XGBoost, LightGBM ou Random Forest em produção caso ofereçam melhor equilíbrio entre recall e taxa de falsos positivos.

Verificar:

- Custo computacional
- Possibilidade de explainability (SHAP)
- Necessidade de re-treino periódico

**5. Dashboards e Acompanhamento**

Criar painéis com:

- AUC ao longo do tempo
- Recall por faixas de score
- Volume diário/semanal de alertas
- Falsos positivos por cluster de clientes
- Conversão de alerta → fraude confirmada

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
