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

- Marca;
- Modelo;
- Idade do Veículo.

### Variáveis Externas

 427 variáveis do catálogo do [[Neurolake]]  e outras variáveis brutas que não fazem parte do catálogo