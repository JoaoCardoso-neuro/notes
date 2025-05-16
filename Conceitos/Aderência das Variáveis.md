---
aliases:
  - Aderência
tags:
  - conceitos
  - processos
---

---

## Conceito

Checagem da variação das variáveis entre duas bases (teste e treino)

## Aderência Categórica
Aderência das variáveis categóricas

### Chi-quadrado:
Teste de hipótese em que verifica se se os valores únicos de uma variável entre duas bases é o mesmo, **quanto maior o chi-square maior a diferença entre as duas bases**

```python
# Set para contagem de valores únicos
df01_set = df01['georcep145c00v01'].value_counts()
df02_set = df02['georcep145c00v01'].value_counts()
# Dataframe
chi = pd.DataFrame(data = {'cat': df01_set.index, 'df01': df01_set.values, 'df02': df02_set.values})
# Valor Chi-square
from scipy.stats import chi2_contingency
treino = chi['df01']
teste = chi['df02']
stat, p, dof, expected = chi2_contingency([treino, teste])
# Resultados
print(f"Estatístico Qui-Quadrado: {stat:.4f}")
print(f"p-valor: {p:.4f}")
print(f"Graus de liberdade: {dof}")
print("Frequências esperadas (baseadas no treino):", expected)
```
### Total Variation 1:
Mede a variação da distribuição dos valores da variável entre as duas bases, **quanto maior, maior a diferença entre as duas bases**

```python
# Set para contagem de valores únicos
df01_set = df01['VARIAVEL'].value_counts(normalize=True)
df02_set = df01['VARIAVEL'].value_counts(normalize=True)
# Dataframe
tv = pd.DataFrame(data = {'cat': df01_set.index, 'df01': df01_set.values, 'df02': df02_set.values})
# Valor do TV1
valor_tv = 0.5*(abs(tv['df01'] - tv['df02']).sum())
valor_tv
```
### Total Variation 2:
Mede a distribuição dos valores da variável entre alvo = 0 e alvo = 1, **quanto maior, mais a variável segmenta o alvo**

``` python
# Set para contagem de valores únicos
df01_0 = df01[df01['TARGET'] == 0]
df01_0 = df01_0['VARIAVEL'].value_counts(normalize=True)
df01_1 = df01[df01['TARGET'] == 1]
df01_1 = df01_1['VARIAVEL'].value_counts(normalize=True)
# Dataframe
tv2 = pd.DataFrame(data = {'cat': df01_0.index, 'df01 = 0': df01_0.values, 'df01 = 1': df01_1.values})
# Valor TV2
valor_tv2 = 0.5*(abs(tv2['df01 = 0'] - tv2['df01 = 1']).sum())
```
### Perc Not Null:
Percentual de não-nulos, ideal é fazer uma diferença em módulo das duas bases verificar **quanto maior a diferença pior para o modelo**

### Q-factor:
Método para comparar os KS2 de uma variável, **quanto menor mais o ks2 varia**

## Aderência Numérica
Aderência das variáveis numéricas

### KS1:
Mede a variação da distribuição dos valores da variável entre as duas bases, **quanto maior, maior a diferença entre as duas bases**

### Desvio Padrão (Std):
Medida de quanto os valores de uma coluna variam, **quanto menor, menos a variável contem informação***

### Perc Not Null:
Percentual de não-nulos, ideal é fazer uma diferença em módulo das duas bases verificar **quanto maior a diferença pior para o modelo**

### KS2:
Mede a distribuição dos valores da variável entre alvo = 0 e alvo = 1, **quanto maior, mais a variável segmenta o alvo**