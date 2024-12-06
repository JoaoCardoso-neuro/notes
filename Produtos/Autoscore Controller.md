---
aliases:
  - Controller
tags:
  - produtos
---

---

## Conceito

Pontuação calculada no momento da cotação que indica a probabilidade de um dado registro estar ou não tentando manipular a cotação. Essa pontuação pode ser usada como um agravo de [Prêmio](Indenização,%20prêmio%20e%20sinistralidade.md) nas cotações mais manipuladas.

Essa pontuação é calculada através de um modelo estatístico de regressão que funciona online para o público de cotações.

## Entendimento e Preparação dos Dados

### Variáveis Internas

Variáveis fornecidas pela seguradora
- NUM_CALCULO
- DAT_RASTR_CALCULO
- SIG_CHASSI
- NUM_CNPJ_CPF_SEGDO
- DAT_INIC_VIGENCIA
- COD_CAT_TARIFA
- DAT_ULT_ALT
- COD_MARCA_TIPO
- FLG_VEICULO_NOVO
- ANO_MODELO
- NUM_CEP_TARIFA
- DAT_NASC_SEGDO
- COD_CLASSE_BONUS
- NUM_PROPOSTA
- COD_CIA_EMIS
- NUM_CPF_CONDUTOR
- DAT_NASC_CONDUTOR
- COD_SEGMENTO_AUTO
- COD_TIPO_RENOVACAO
- COD_USO_VEIC
- VAL_IS_CASCO
- VAL_PREM_LIQ
- IDC_TIPO_PESSOA
- FLG_CONDUTOR_18_25ANOS
- IDC_QAR
- IDC_TIPO_CONTR
- SIG_FABRIC
- f_proposta
- f_frota

### Variáveis Externas

Variáveis  que compreendem todo o catálogo do [[Neurolake]], além de variáveis brutas que não fazem parte do catálogo. Exemplos: SCORE_RISCO_CADASTRAL,  SCORE_RISCO_WEB, COMPARATIVO_RENDA.