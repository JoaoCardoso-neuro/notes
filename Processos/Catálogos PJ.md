---
aliases:
  - Catálogo 3.1
  - Catálogo 3.2
  - Catálogo 3.4
  - "3.1"
  - "3.2"
  - "3.4"
  - Empresarial
tags:
  - processos
  - ferramentas
---
---
## O que é

Processos de enriquecimento de dados, através do [Postman](Postman.md) para os produtos de seguros de propriedade para CNPJs (Property PJ)
## Scripts API

### 3.1
```javascript
{

"step_type": "spark-submit",

"args_step": [

"spark-submit",

"--deploy-mode", "cluster",

"--driver-memory", "20G",

"--executor-cores", "3",

"--executor-memory", "15G",

"--conf", "spark.sql.broadcastTimeout=1200",

"--conf", "spark.yard.maxAppAttempts=1",

"--conf", "spark.driver.maxResultSize=2048MB",

"s3://dev-neurolake/config/BIGDATACODE/book/cardapio_PJ_3.1.py",

"s3://dev-neurolake-sftp/seguros-auto/dev-seguros/Bases/HDI/2025-01-13/bases/chave_bz2",

"sandbox.catalogo31_hdi_score_empresarial_20250113",

"-kc", "NroCpfCnpj",

"-cep", "CodCEP",

"-dc", "DATA_EMISSAO", "yyyy-MM-dd"

],

"squad_name": "SEGUROS_AUTO",

"job_id":"ENRIQUECIMENTO_CATALOGO_PJ_3_1",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D",

"client":"HDI",

"project":"SCORE",

"product":"EMPRESARIAL",

"squad": "SEGUROS_AUTO",

"environment": "PRD",

"createdby": "JVCS"

}
```
### 3.2

```javascript
{

"step_type": "spark-submit",

"args_step": [

"spark-submit",

"--deploy-mode", "cluster",

"--driver-memory", "20G",

"--executor-cores", "3",

"--executor-memory", "15G",

"--conf", "spark.sql.broadcastTimeout=1200",

"--conf", "spark.yard.maxAppAttempts=1",

"--conf", "spark.driver.maxResultSize=2048MB",

"s3://dev-neurolake/config/BIGDATACODE/book/cardapio_PJ_3.2.py",

"s3://dev-neurolake-sftp/seguros-auto/dev-seguros/Bases/HDI/2025-01-13/bases/chave_bz2",

"sandbox.catalogo32_hdi_score_empresarial_20250113",

"-kc", "NroCpfCnpj",

"-cep", "CodCEP",

"-dc", "DATA_EMISSAO", "yyyy-MM-dd"

],

"squad_name": "SEGUROS_AUTO",

"job_id":"ENRIQUECIMENTO_CATALOGO_PJ_3_2",

"google_chat_url": "https://chat.googleapis.com/v1/spaces/AAAAZAtf4Xo/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=DF8DWXEgBTwtlemI4avQ4plHdwsjUe_CQh8qqbLvONg%3D",

"client":"HDI",

"project":"SCORE",

"product":"EMPRESARIAL",

"squad": "SEGUROS_AUTO",

"environment": "PRD",

"createdby": "JVCS"

}
```

### 3.4

```javascript
{

"cluster_type": "emr_split_default",

"step_type":"papermill",

"pm_params": {

"input_table": "seguros.base_hdi_score_empresarial_20250113_chave",

"output_table": "sandbox.catalogo34_hdi_score_empresarial_20250113_full",

"key_column": "NroCpfCnpj",

"ref_date_column": "DATA_EMISSAO",

"cep_column": "CodCEP",

"ref_date_mask": "yyyy-MM-dd",

"geo_columns": "True",

"write_mode": "append"

},

"args_step": [

"codecommit://neurolake-dados-notebooks/books/CATALOGO_PJ/CATALOGO_PJ_3_4.ipynb"

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