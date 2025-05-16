---
aliases:
  - Autoscore RF Liberty
  - Autoscore Sinistro Liberty
tags:
  - processos
  - produtos
---
---
## Resumo

Para o [Autoscore RF](Autoscore%20Roubo%20e%20Furto.md) e [Autoscore Sinistro](Autoscore%20Sinistro.md) da Liberty, após a validação da base, deve-se enriquecer com o script do [Postman](Postman.md) da Liberty e então dar um join da base enriquecida com a original, é importante criar uma flag de enriquecido 0 ou 1 já que podem haver registros que não foram enriquecidos.

Após o enriquecimento, para o caso da Liberty, precisamos adicionar as colunas ANO_FABRICACAO, MODELO e IDADE_VEICULO para que possamos escorar com os modelos. O modelo de [Sinistro](Autoscore%20Sinistro.md) é um PMML por isso precisamos rodar o [Prophet](Prophet.md) antigo, no código deste modelo só precisa-se mudar o final do arquivo contendo a base fonte e o nome da base escorada que o modelo irá salvar. Já para o modelo de [RF](Autoscore%20Roubo%20e%20Furto.md) seguimos o processo normal da base [[ONNX]] (sem as colunas adicionadas anteriormente). 

Finalmente unem-se as bases escoradas com a base original e as variáveis que o cliente solicitar (por padrão CLASSE_SOCIAL, IDADE e SCORE_RISCO_CADASTRAL do catálogo da HDI) juntamente com a coluna de flag de enriquecimento, pois para os casos que não foram enriquecidos precisamos atribuir o score -1.

## Fluxograma

```mermaid
%%{init: {"flowchart": {"htmlLabels": false}} }%% 
flowchart TB
id1[Validar Base]
id2["Enriquecimento Liberty"]
id3["Join Base Enriq + Original"]
id4["Adicionar colunas 
(IDADE_VEICULO, MODELO 
e ANO_FABRICACAO)"]
id5["Escorar Sinistro (PMML)"]
id6["Escorar RF (ONNX)"]
id7["Join Scores + Variáveis"]
id8["Comparar Diist. e Nulls"]
id9["Retornar ao Cliente"]
id1 --> id2 --> id3 --> id4 --> id5 --> id6 --> id7 --> id8 --> id9
```

## Script

```javascript
{

"step_type": "papermill",

"pm_params": {

"path": "seguros.base_hdi_autoscore_20250114",

"cpf_column": "NroCPFCNPJ",

"cep_column": "CepPernoite",

"output_path": "sandbox.as30_hdi_liberty_autoscore_20250114_prod"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/LIBERTY_PROD.ipynb"],

"cluster_type": "emr_split_default",

"job_id": "LIBERTY_ENRIQ_PROD",

"squad_name": "SEGUROS_AUTO",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D"

}
```