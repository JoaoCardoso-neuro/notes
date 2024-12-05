---
aliases:
  - GB
  - Boosting Trees
  - Bossting
tags:
  - conceitos
---

---

## Conceito

Método de machine learning que combina várias árvores de decisão mais fracas para criar um modelo mais robusto, esse processo é feito de forma sequencial onde cada árvore tenta corrigir o erro da anterior

O primeiro passo tomado pelo algoritmo em problemas de regressão por exemplo é calcular a média da variável target, então com os residuais (variável prevista - variável observada) é feita uma árvore de decisão para prever os residuais

Então a variável target prevista seria a média + os residuais multiplicados pelo fator de learning rate (para evitar overfit)


## Parâmetros

### max_leaves ou max_depth:

Número máximo de folhas de cada node

### learning_rate ou eta:

Fator multiplicado pelos residuais para evitar overfit