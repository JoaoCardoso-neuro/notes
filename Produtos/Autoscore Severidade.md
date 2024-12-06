---
aliases:
  - Severidade
tags:
  - produtos
---

---

## Conceito

Modelo estatístico de regressão que funciona online. É uma estimativa do impacto econômico que o CPF pode gerar a seguradora, é calculado pela fórmula abaixo

$$
ValorSeveridade = \frac{\sum{Idenizacoes}}{ValorCasco} 
$$

## Entendimento e Preparação dos Dados

Chave de identificação:
- CPF;
- CEP;
- Data Início Vigência;
- Marca;
- Modelo;
- Ano de Fabricação;
- Valor do casco.

**Alvo numérico: valor da severidade**

### Variáveis Internas

Variáveis fornecidas pela seguradora
- Marca;
- Modelo;
- Idade do Veículo;
- Valor do Casco.

### Variáveis Externas

144 variáveis do catálogo do [[Neurolake]] e outras variáveis brutas que não fazem parte do catálogo

## Avaliação de Desempenho

Em uma base de testes tem-se o resultado abaixo:

<img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfTW1XWnW9Bh9d0zgSsVM0B_Bf6Mm18kkPQe1ETlcB1HMIxhG8nC7zEMShtqG8lryWGmFDT811iaOmUmT8MQnbhWvtebDuGPhkximrzEcfGnBG8N_ILCNaDuwdZS2PoE3yBOPDDccvfLq7ZuHhrK-BvWY0?key=d6rKKttZVhVn00IuKV9ppg" width="650" />

Nesse gráfico a base de apólices foi separada em dez faixas (decis) e ordenadas pelo score de severidade. Em seguida a taxa real de conversão foi calculada em cada faixa. Portanto, podemos observar que, nos scores mais altos, a taxa de severidade é maior e nos mais baixos a taxa de severidade é menor
