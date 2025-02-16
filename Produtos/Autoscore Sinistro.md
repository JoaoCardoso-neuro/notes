---
aliases:
  - Sinistro
tags:
  - produtos
---
---
## Conceito

Modelo de classificação binária com funcionamento online para o público de cotações de seguros que indica o potencial do CPF sofrer qualquer tipo de sinistro durante a vigência do seguro 

## Entendimento e Preparação dos Dados

Chave de identificação:
- CPF;
- CEP;
- Data Início Vigência;
- Marca;
- Modelo;
- Ano de Fabricação.

**Alvo binário: sofreu sinistro sim ou não**

### Variáveis Internas

Variáveis fornecidas pela seguradora
- Marca;
- Modelo;
- Idade do Veículo.

### Variáveis Externas

44 variáveis do catálogo do [[Neurolake]]  e outras variáveis brutas que não fazem parte do catálogo

## Modelagem

A modelagem foi feita através das soluções [[Hydra]], [[Flame]] e [[Prophet]]. O treinamento dos modelos é realizado no AWS, os modelos podem ser exportados em formato [[ONNX]] 

## Avaliação de Desempenho

Em uma base de testes tem-se o resultado abaixo:

<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcp8JkfMjzGwW2H55MRiuAeSmbwgoiIyVRnCpMUvmID42TbfjwLu1caQ00UL8h3SP6XJOe5GoBVpRP7XhR9oL_kotRGFQfUXolh1-4cEISUAcyG8fCIBcJYX1-_gGCVvSVEFLb3s-ejp3B6RnbK5hv4JII?key=d6rKKttZVhVn00IuKV9ppg" width="650" />

Nesse gráfico a base de apólices foi separada em dez faixas (decis) e ordenadas pelo score de sinistro. Em seguida a taxa real de sinistro foi calculada em cada faixa. Portanto, podemos observar que, nos scores mais altos, a taxa de sinistro é maior e nos mais baixos a taxa de sinistro é menor