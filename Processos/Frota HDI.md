---
aliases:
  - Autoscore Frota HDI
tags:
  - processos
  - produtos
---
---
## Resumo

O enriquecimento de Frota da HDI consiste em entregar o [Autoscore Sinistro](Autoscore%20Sinistro.md) PF, [Autoscore Roubo e Furto](Autoscore%20Roubo%20e%20Furto.md) PF, [[Autoscore Perda Parcial]] PJ e [Autoscore Roubo e Furto](Autoscore%20Roubo%20e%20Furto.md) PJ além de algumas variáveis como IDADE, SCORE_RISCO_CADASTRAL, GENERO, PORTE_FATURAMENTO_PRESUMIDO, PORTE, DISTANCIA_AGLOMERADO_SUBNORMAL, TEMPO_ATIVIDADE, SECAO_CNAE e CNAE_PRINCIPAL.

Após a validação da base devem-se realizar 2 enriquecimentos: Enriquecimento de CEP e Enriquecimento do Catálogo 3.4 PJ com os enriquecimentos em mãos precisa-se fazer o join com a base original para assim seguir para os próximos enriquecimentos.

Os enriquecimentos seguintes são os catálogos PF, PJ para Perda Parcial, PJ para Perda Total e Roubo e Furto e catálogo PF 2.0. Após os enriquecimentos, deve ser dado um join com cada base e a base do primeiro enriquecimento. Em seguida podemos efetuar o recall dos experimentos em cada base e acrescentar na base as variáveis de retorno e comparar a distribuição dos scores com bases de referência e verificar o percentual de nulos das variáveis a serem retornadas

**Variáveis:
- **Catálogo 2.0:**
  IDADE
  GENERO
  DISTANCIA_AGLOMERADO_SUBNORMAL_PF
  SCORE_RISCO_CADASTRAL
- **Catálogo 3.4:**
  DISTANCIA_AGLOMERADO_SUBNORMAL_PJ
  CNAE_PRINCIPAL
  TEMPO_ATIVIDADE
  SECAO_CNAE
  PORTE_FATURAMENTO_PRESUMIDO
  PORTE

## Fluxograma

```mermaid
%%{init: {"flowchart": {"htmlLabels": false}} }%% 
flowchart TB
id1["Validar Base"]
id2["Enriquecer com CEP"]
id3["Enriquecer Catálogo 3.4"]
id4["Join Bases Enriq 1 + Orig"]
id5["Enriquecimento Catálogo PF"]
id6["Enriquecimento Catálogo PJ (PP)"]
id7["Enriquecimento Catálogo PJ (PT e RF)"]
id8["Enriquecimento Catálogo PF 2.0"]
id9["Join Bases Enriq 2 + Enriq 1"]
id10["Escorar Cada Modelo Separado"]
id11["Join Scores e Variávies"]
id12["Comparar Dist. e Nulls"]
id13["Retornar ao Cliente"]
id1 --> id2 --> id3 --> id4 --> id5 --> id6 --> id7 --> id8 --> id9 --> id10 --> id11 --> id12 --> id13
```

## Scripts

### Enriquecimento CEP

```javascript
{

"cluster_type": "emr_split_default",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D",

"job_id": "ENRIQ_CEP",

"pm_params": {

  

"input_path": "seguros.base_enriq_banco_pan_20250227",

"output_path": "sandbox.cep_base_enriq_banco_pan_20250227",

"key_column": "CHAVE",

"cpf_column": "cpf",

"ref_date_column": "data_ref",

"ref_date_mask": "yyyy-MM-dd"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/ENRIQ_CEP.ipynb"],

"squad_name": "SEGUROS_AUTO",

"step_type": "papermill"

}
```

### Enriquecimento Catálogo 3.4

```javascript
{

"cluster_type": "emr_split_default",

"step_type":"papermill",

"pm_params": {

"input_table": "seguros.base_hdi_autoscore_frota_20250207",

"output_table": "sandbox.catalogo34_hdi_score_empresarial_20250207",

"key_column": "NroCpfCnpj",

"ref_date_column": "REF_DATE",

"cep_column": "None",

"ref_date_mask": "yyyy-MM-dd",

"geo_columns": "True",

"write_mode": "append"

},

"args_step": [

"codecommit://neurolake-dados-notebooks/books/CATALOGO_PJ/CATALOGO_PJ_3_4.ipynb",

"s3://dev-neurolake-notebook/jupyter/mvca/HDI/2023-12-18/2-EnriquecimentoPF/"

],

"squad_name": "SEGUROS_AUTO",

"job_id":"ENRIQUECIMENTO_CATALOGO_PJ_3_4",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D",

"client":"HDI",

"project":"SCORE",

"product":"EMPRESARIAL",

"squad": "SEGUROS_AUTO",

"environment": "PRD",

"createdby": "JVCS"

}
```

### Enriquecimento Catálogo PF

```javascript
{

"step_type": "papermill",

"pm_params": {

"path": "seguros.base_hdi_autoscore_frota_20250207_cep",

"cpf_column": "NroCpfCnpj",

"cep_column": "CEP",

"output_path": "sandbox.as30_hdi_autoscore_frota_20250210_prod"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/HDI_PROD_PF_30_SIN_RF.ipynb"],

"cluster_type": "emr_split_default",

"job_id": "HDI_ENRIQ_FROTA_PF_PROD",

"squad_name": "SEGUROS_AUTO",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D"

}
```

### Enriquecimento Catálogo PJ Perda Parcial

```javascript
{

"step_type": "papermill",

"pm_params": {

"path": "seguros.base_hdi_autoscore_frota_20250207_cep_pj",

"cnpj_column": "NroCpfCnpj",

"cep_column": "CEP",

"output_path": "sandbox.as30_pj_pp_hdi_autoscore_frota_20250210_prod"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/HDI_PROD_PJ_30_PP.ipynb"],

"cluster_type": "emr_split_default",

"job_id": "HDI_ENRIQ_FROTA_PJ_PP_PROD",

"squad_name": "SEGUROS_AUTO",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D"

}
```

### Enriquecimento Catálogo PJ Roubo e Furto e Perda Total

```javascript
{

"step_type": "papermill",

"pm_params": {

"path": "seguros.base_hdi_autoscore_frota_20250207_cep_pj",

"cnpj_column": "NroCpfCnpj",

"cep_column": "CEP",

"output_path": "sandbox.as30_pj_rf_hdi_autoscore_frota_20250210_prod"

},

"args_step": ["codecommit://seguros-auto-notebooks/enriquecimentos/HDI_PROD_PJ_30_PT_RF.ipynb"],

"cluster_type": "emr_split_default",

"job_id": "HDI_ENRIQ_FROTA_PJ_RF_PT_PROD",

"squad_name": "SEGUROS_AUTO",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D"

}
```

### Enriquecimento Catálogo PF 2.0

```javascript
{'squad_name': 'SEGUROS_AUTO',
 'Environment': 'PRD',
 'Project': 'CATALOGO',
 'Product': 'CATALOGO_PF',
 'Squad': 'SEGUROS_AUTO',
 'CreatedBy': 'WAS',
 'conf': {'client': 'HDI',
  'pasta_data': 'enriquecimento_hdi_autoscore_frota_20250210',
  'col_cpf': 'NroCpfCnpj',
  'col_ref_date': 'REF_DATE',
  'format_ref_date': 'yyyy-MM-dd',
  'cep': 'CEP',
  'base_bruta': 's3://dev-neurolake-sftp/seguros-auto/dev-seguros/Bases/HDI/2025-02-07/base_cep',
  'separador': '\t',
  'segmento': 'SEGURO_AUTO',
  'equipe': 'growth'}}
```
