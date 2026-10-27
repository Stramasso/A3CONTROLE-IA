# Controle de irrigação com rede neural e lógica fuzzy

Projeto semestral (A3) da unidade curricular de Sistemas de Controle e Inteligência Artificial da Universidade São Judas Tadeu.

O objetivo é decidir quando ligar a bomba de água de uma irrigação a partir de três leituras de sensores: **umidade do solo**, **temperatura** e **umidade do ar**. O problema foi atacado de duas formas, para comparar uma abordagem orientada a dados com uma baseada em regras.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Stramasso/A3CONTROLE-IA/blob/main/projeto_a3_sistemasdecontrole_ia.ipynb)

## Dados

[`dados_irrigacao.csv`](dados_irrigacao.csv) tem 3.000 leituras com as três variáveis de entrada e o estado da bomba (0 = desligada, 1 = ligada). As classes são praticamente balanceadas.

## Abordagens

**1. Rede neural (MLP)**

- Análise exploratória: valores ausentes, estatísticas descritivas, boxplots, histogramas e gráfico de dispersão por classe
- Padronização com `StandardScaler` e divisão treino/teste 80/20
- `MLPClassifier` com duas camadas ocultas (16 e 8 neurônios, ReLU, Adam)
- Resultado: acurácia de 99,8% no teste (1 erro em 600 amostras). Um valor tão alto indica que o estado da bomba no conjunto de dados segue uma regra quase determinística sobre as entradas, o que é discutido no notebook

**2. Controlador fuzzy**

- Entradas e saída modeladas com funções de pertinência trapezoidais (baixa, média, alta / desligada, ligada)
- 27 regras cobrindo todas as combinações, com prioridade umidade do solo > temperatura > umidade do ar
- A saída é a porcentagem de acionamento da bomba, convertida em vazão (m³/h) a partir da vazão máxima do equipamento

## Tecnologias

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · scikit-fuzzy · Google Colab

## Como executar

Abra o notebook no Colab pelo botão acima e, na primeira célula, envie o arquivo `dados_irrigacao.csv` quando for solicitado.
