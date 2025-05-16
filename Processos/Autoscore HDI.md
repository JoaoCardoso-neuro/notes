---
aliases:
  - Autoscore RF HDI
  - Autoscore Sinistro HDI
tags:
  - processos
  - produtos
---
---
## Resumo

Para o [Autoscore RF](Autoscore%20Roubo%20e%20Furto.md) e [Autoscore Sinistro](Autoscore%20Sinistro.md) da HDI, após a validação da base, deve-se enriquecer com o script do [Postman](Postman.md) da HDI e então dar um join da base enriquecida com a base original, é importante criar uma flag de enriquecido 0 ou 1 já que podem haver registros que não foram enriquecidos.

Com a base enriquecida escora-se cada modelo ([ONNX](ONNX.md)) separadamente salvando-os, posteriormente é feito um join nestas duas bases juntamente com as variáveis que o cliente solicitou (por padrão CLASSE_SOCIAL, IDADE e SCORE_RISCO_CADASTRAL) e com a coluna de flag de enriquecimento, pois para os casos que não foram enriquecidos precisamos atribuir o score -1.

**Obs:** Por padrão retornamos o [[Autoscore Liberty]] junto com o da HDI

## Fluxograma

```mermaid
%%{init: {"flowchart": {"htmlLabels": false}} }%% 
flowchart TB
id1[Validar Base]
id2["Enriquecimento HDI"]
id3["Join Base Enriq + Original"]
id4["Escorar Cada Modelo Separado"]
id5["Join Scores e Variaveis"]
id6["Comparar Dist. e Nulls"]
id7["Retornar ao Cliente"]
id1 --> id2 --> id3 --> id4 --> id5 --> id6 --> id7
```

## Script

```javascript
{

"step_type": "papermill",

"pm_params": {

"path": "seguros.base_hdi_autoscore_20250114",

"cep_column": "CepPernoite",

"output_path": "sandbox.as40_hdi_liberty_autoscore_20250114_prod"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/HDI_PROD.ipynb"],

"cluster_type": "emr_split_default",

"job_id": "HDI_ENRIQ_PROD",

"squad_name": "SEGUROS_AUTO",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D"

}
```