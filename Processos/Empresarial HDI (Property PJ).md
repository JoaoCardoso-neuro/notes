---
aliases:
  - Property HDI
  - Property PJ HDI
tags:
  - processos
  - produtos
---
---
## Resumo

Para o enriquecimento do catálogo de property da HDI primeiramente deve-se validar a base verificando se todas as colunas necessárias (CNPJ, CEP e Data) estão presentes, rodar os scripts no [Postman](Postman.md) dos catálogos [3.1](Catálogos%20PJ.md) para RF e Danos Elétricos e [3.2](Catálogos%20PJ.md) para Vendaval, além disso rodar o [3.4](Catálogos%20PJ.md) para retorar as variáveis que eles necessitam (PORTE, SCORE_RISCO_GEORREFERENCIADO, TEMPO_ATIVIDADE, SECAO_CNAE) pois é o catálogo mais atualizado.

Após rodar os enriquecimentos escoram-se as bases correspondentes de cada um com os modelos ([ONNX](ONNX.md)) também correspondentes. Após a escoragem precisa-se dar um join nas 3 bases para criar a base para o retorno e comparar a distribuição dos scores e o percentual de nulo das variáveis.

## Fluxograma

```mermaid
%%{init: {"flowchart": {"htmlLabels": false}} }%% 
flowchart TB
id1[Validar Base]
id2["Enriquecer Catálogo 3.1 
(RF e Danos Elétricos)"]
id3["Enriquecer Catálogo 3.2
(Vendaval)"]
id4["Enriquecer Catálogo 3.4
(Variáveis)"]
id5["Escorar Cada Base Separada"]
id6["Join Scores e Variaveis"]
id7["Comparar Dist. e Nulls"]
id8["Retornar ao Cliente"]
id1 --> id2 --> id3 --> id4 --> id5 --> id6 --> id7 --> id8
```
