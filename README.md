# Detecção de Fraudes em Transações de Cartão de Crédito

Projeto de Machine Learning desenvolvido para identificar possíveis fraudes em transações de cartão de crédito.

O projeto foi desenvolvido como parte de um desafio prático de Data Science, explorando um problema real de classificação com forte desbalanceamento entre as classes.

## Objetivo

Construir modelos capazes de identificar transações fraudulentas e analisar seu desempenho utilizando métricas adequadas para problemas de classificação desbalanceada.

O projeto também busca interpretar as decisões do modelo utilizando SHAP.

## Problema

O dataset possui uma quantidade muito maior de transações legítimas do que fraudulentas.

A distribuição encontrada foi aproximadamente:

* **99,83%** de transações legítimas
* **0,17%** de transações fraudulentas

Por esse motivo, a acurácia isoladamente não é suficiente para avaliar o modelo.

As principais métricas utilizadas foram:

* Precisão (Precision)
* Recall
* F1-Score

## Dataset

Foi utilizado o dataset de transações de cartão de crédito disponibilizado pelo TensorFlow.

A base possui:

* 284.807 transações
* 30 variáveis preditoras
* 1 variável alvo (`Class`)

A variável `Class` representa:

* `0` → transação legítima
* `1` → transação fraudulenta

O dataset não é armazenado neste repositório. Ele é carregado diretamente pela URL no notebook.

## Tecnologias utilizadas

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* SHAP
* Matplotlib
* Google Colab

## Etapas do projeto

### 1. Exploração dos dados

Foi realizada uma análise inicial da estrutura da base, incluindo:

* dimensões;
* tipos das variáveis;
* distribuição da classe alvo;
* identificação do desbalanceamento.

### 2. Preparação dos dados

Os dados foram separados entre variáveis preditoras (`X`) e variável alvo (`y`).

Também foi utilizado `train_test_split` com `stratify`, garantindo a preservação da proporção das classes nos conjuntos de treinamento e teste.

As variáveis `Time` e `Amount` foram padronizadas utilizando `StandardScaler`.

### 3. Modelos

Foram treinados três modelos de classificação:

* Regressão Logística
* Random Forest
* XGBoost

Para lidar com o desbalanceamento, foram utilizadas técnicas de ponderação das classes.

### 4. Comparação dos modelos

Os modelos foram avaliados utilizando a classe de fraude como principal foco.

| Modelo              | Precisão | Recall | F1-Score |
| ------------------- | -------: | -----: | -------: |
| Regressão Logística |   0,0610 | 0,9184 |   0,1144 |
| Random Forest       |   0,9605 | 0,7449 |   0,8391 |
| XGBoost             |   0,7368 | 0,8571 |   0,7925 |

Os resultados demonstram diferentes comportamentos entre os modelos.

A Regressão Logística apresentou maior recall, porém com baixa precisão. O Random Forest apresentou alta precisão, mas menor recall. O XGBoost apresentou um recall maior que o Random Forest, enquanto o Random Forest apresentou maior precisão e F1-Score.

### 5. Ajuste do threshold

Além do threshold padrão de 0,5, foram testados diferentes valores entre 0,1 e 0,9.

Entre os valores avaliados, o threshold de **0,8** apresentou o maior F1-Score:

* Precisão: **87,91%**
* Recall: **81,63%**
* F1-Score: **84,66%**

O ajuste demonstra que o threshold pode alterar significativamente o equilíbrio entre identificação de fraudes e geração de falsos positivos.

### 6. Curvas ROC e Precision-Recall

Foram utilizadas as curvas ROC e Precision-Recall para complementar a avaliação dos modelos.

A curva Precision-Recall possui importância especial neste projeto devido ao forte desbalanceamento da base e ao foco na identificação da classe de fraude.

### 7. Explicabilidade com SHAP

O SHAP foi utilizado para interpretar as decisões do XGBoost.

A análise global indicou que variáveis como:

* V14
* V4
* V12
* V10
* V3
* V11

apresentaram grande influência nas previsões do modelo.

Também foi realizada uma análise individual de uma transação para observar como diferentes variáveis contribuíram para a decisão do modelo.

É importante destacar que as contribuições apresentadas pelo SHAP representam a influência das variáveis na previsão do modelo, não uma relação de causalidade.

## Conclusão

O projeto demonstrou um pipeline completo de Machine Learning aplicado à detecção de fraudes.

O principal desafio encontrado foi o forte desbalanceamento entre as classes, tornando necessário analisar métricas além da acurácia.

A comparação entre os modelos mostrou que diferentes algoritmos apresentam diferentes relações entre precisão e recall. O ajuste do threshold também demonstrou que o ponto de decisão pode ser alterado de acordo com o objetivo da aplicação.

A utilização do SHAP complementou a análise ao permitir interpretar as variáveis que mais contribuíram para as previsões do XGBoost.

## Como executar

1. Clone este repositório.
2. Abra o arquivo `deteccao_fraude_cartao.ipynb`.
3. Execute o notebook no Google Colab ou em um ambiente Python compatível.
4. O dataset será carregado automaticamente pela URL utilizada no notebook.

## Estrutura do projeto

```text
deteccao-fraude-cartao/
│
├── deteccao_fraude_cartao.ipynb
└── README.md
```
