---
aliases:
  - OHE
  - One-hot
tags:
  - conceitos
---
---
## Conceito

Codificador utilizado naa etapa de pré-processamento que transforma variáveis categóricas em numéricas. O one-hot transforma valor único de uma variável em um coluna na base de dados

## Exemplo

| **Cor**  | Azul | Verde | Vermelho |
| -------- | ---- | ----- | -------- |
| Azul     | 1    | 0     | 0        |
| Verde    | 0    | 1     | 0        |
| Vermelho | 0    | 0     | 1        |
| Azul     | 1    | 0     | 0        |
## Código

```python
from sklearn import OneHotEncoder()
enc = OneHotEncoder(handle_unknown='ignore')
X = [['Male', 1], ['Female', 3], ['Female', 2]]
enc.fit(X)
```
