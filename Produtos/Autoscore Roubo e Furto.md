---
aliases:
  - Autoscore RF
  - RF
tags:
  - produtos
---

---

## Conceito

Modelo de classificação binária com funcionamento online para os clientes de cotações de seguro. O modelo gera uma pontuação que indica o potencial do CPF ser roubado ou furtado durante a vigência do seguro

## Entendimento e Preparação dos Dados

Chave de identificação:
- CPF;
- CEP;
- Data Início Vigência;
- Marca;
- Modelo;
- Ano de Fabricação.

**Alvo binário: furto sim ou não**

### Variáveis Internas:

Variáveis fornecidas pela seguradora
- Marca;
- Modelo;
- Idade do Veículo.

### Variáveis Externas

144 variáveis do catálogo do [[Neurolake]]  e outras variáveis brutas que não fazem parte do catálogo

## Modelagem

A modelagem foi feita através das soluções [[Hydra]], [[Flame]] e [[Prophet]]. O treinamento dos modelos é realizado no AWS, os modelos podem ser exportados em formato [[ONNX]] 

## Avaliação de Desempenho

Em uma base de testes tem-se o resultado abaixo:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeonAQDDPI5XL-iK1-ftG_y2n_EVwmhd4sniJR3MUiDYMMXzj7h7AUiBiVIz2jeJ5OAXkMKcw0sH5wOUWITUHMmfgoK_JPcV_IwUO6UAFejSZar8lcUoeHyvJiTISuY-vzcx-wSROifCA5oAudrwuMaJg?key=d6rKKttZVhVn00IuKV9ppg)

Nesse gráfico a base de apólices foi separada em dez faixas (decis) e em seguida a taxa real de roubo e furto foi calculada em cada faixa. Portanto, podemos observar que, quanto maior as observações menor a taxa de RF

Espera-se que os modelos de autoscore RF se comportem dessa maneira
