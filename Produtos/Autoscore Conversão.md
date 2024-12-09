---
aliases:
  - Conversão
tags:
  - produtos
---
---
## Conceito

Modelo de classificação binária com funcionamento online para os clientes de cotações de seguro. O modelo gera uma pontuação que indica o potencial do CPF contratar o seguro (conversão). Além das variáveis padrão, o modelo calcula um desconto ou agravo. Cotações com baixo potencial de conversão recebem um desconto no preço e com alto potencial recebem um agravo.

## Entendimento e Preparação dos Dados

Chave de identificação:
- CPF;
- CEP;
- Data Cotação;
- Marca;
- Modelo;
- Ano de Fabricação.

**Alvo binário: converteu sim ou não**

### Variáveis Internas

Variáveis fornecidas pela seguradora
- Marca;
- Modelo;
- Idade do Veículo.

### Variáveis Externas

 427 variáveis do catálogo do [[Neurolake]]  e outras variáveis brutas que não fazem parte do catálogo
 
## Modelagem

A modelagem foi feita através das soluções [[Hydra]], [[Flame]] e [[Prophet]]. O treinamento dos modelos é realizado no AWS, os modelos podem ser exportados em formato [[ONNX]] 

## Avaliação de Desempenho

Em uma base de testes tem-se o resultado abaixo:

<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcThmckj9CP1cziCI8peE0mI8w39XgFvgDIMwgtmnFv5u-KUX3_jvSfRi5CTjRkYdM83eyP69vX9c7BvWw3HiQSsnj3HInpq9cChDzm4DDG1Lpu_nBoT4DISCDGr_Pc1evepz7XtFfuihdLRucPMxn4jJA?key=d6rKKttZVhVn00IuKV9ppg" alt="Descrição da imagem" width="650" />

Nesse gráfico a base de apólices foi separada em dez faixas (decis) e ordenadas pelo score de conversão. Em seguida a taxa real de conversão foi calculada em cada faixa. Portanto, podemos observar que, nos scores mais altos, a taxa de conversão é maior e nos mais baixos a taxa de conversão é menor

## Implantação Autoscore Conversão HDI Seguros

A decisão de oferecer desconto ou agravo deve levar em conta também o risco envolvido naquela cotação, por isso leva-se em conta algum produto de risco (como [Autoscore Sinistro](Autoscore%20Sinistro.md) ou [Autoscore Roubo e Furto](Autoscore%20Roubo%20e%20Furto.md)) como parte da decisão

<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdM9JPYssJh7h2jE7PvCKc7WvKgskDgpu120B7N3o77rk__ZImGw1jH8g2LqFX5xFhxMQ_nNnA2D4Gwo31MNrGDC2QiatRZkefLNRqfwXYotgKF1fa7usUfsblcA5gjewImdAdpscRaoakc9W2yBDw0cIA?key=d6rKKttZVhVn00IuK" width="650" />

Essa solução é aplicada em seguros novos ou renovação congênere, cuja média de conversão é 3,3%. Já a taxa de conversão atual do grupo de desconto é 1,4%, esse grupo corresponde a 24% das cotações, a sinistralidade esperada desse grupo é de 69%

Em outras palavras, o desconto no valor é aplicado na combinação dos dois cenários acima e em aproximadamente 24% das cotações. A taxa de desconto varia de 0% a 5%.