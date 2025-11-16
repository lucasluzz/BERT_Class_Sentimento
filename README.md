# 🤖 Classificação de Sentimento com BERT

Este repositório contém o código de um projeto de Inteligência Artificial para classificar o sentimento (positivo, negativo ou neutro) de comentários em português usando o modelo BERT.

O projeto treina **três modelos de classificação independentes** para analisar o sentimento em três tópicos distintos:
1.  Onça
2.  Caseiro
3.  Notícia

O código principal está documentado no notebook Jupyter (`.ipynb`) e foi desenvolvido para ser executado no ambiente Google Colab com aceleração de GPU.

---

## 🎯 Metodologia

O pipeline do projeto segue 5 etapas principais:

1.  **Preparação dos Dados:** Os dados são lidos, limpos e os rótulos de texto (ex: "positivo") são convertidos em números (ex: 2). O conjunto de dados é dividido em **Treino (70%)**, **Validação (15%)** e **Teste (15%)** usando uma divisão estratificada única para evitar vazamento de dados (`data leakage`) entre os três modelos.
2.  **Tokenização:** Usamos o `AutoTokenizer` do modelo `neuralmind/bert-base-português-cased` para converter os textos em tensores (`input_ids` e `attention_mask`) que o BERT entende.
3.  **Modelo:** Carregamos três instâncias independentes de `BertForSequenceClassification` com uma cabeça de classificação de 3 rótulos.
4.  **Treinamento:** Cada modelo é treinado por 10 épocas usando o otimizador `AdamW` (lr=2e-5). O *loss* e a acurácia de treino/validação são monitorados a cada época.
5.  **Avaliação:** Os modelos finais são avaliados no conjunto de teste (15% dos dados nunca vistos) usando o `classification_report` do Scikit-learn para medir Precision, Recall e F1-Score.

---

## 📊 Resultados Finais (Acurácia no Teste)

Os modelos treinados alcançaram os seguintes resultados no conjunto de teste:

| Modelo | Acurácia Geral | F1-Score (Macro Avg) |
| :--- | :---: | :---: |
| **Onça** | 81% | 0.67 |
| **Caseiro** | 87% | 0.68 |
| **Notícia** | 94% | 0.80 |

O modelo **Notícia** foi o de melhor desempenho, demonstrando alta capacidade de generalização para classificar as três classes (boa, ruim, neutra) com eficácia.

---

## 🚀 Como Executar

1.  Abra o arquivo `.ipynb` no [Google Colab](https://colab.research.google.com/).
2.  Certifique-se de que o ambiente de execução está configurado para usar um **acelerador de hardware (GPU)**.
    * (Ambiente de execução -> Alterar o tipo de ambiente de execução -> T4 GPU)
3.  Execute todas as células em ordem.
