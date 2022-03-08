<img src="https://img.carteiraglobal.com/logo-cg.png" alt="logo-cg" style="zoom:50%;float:left;" />

# Challenge Backend

## Objetivos

O objetivo desse Challenge é testar a sua capacidade e criatividade para extrair, transformar e carregar as informações limpas de um site em uma base de dados.

Iremos trabalhar com os dados abertos da CVM - Comissão de Valores Mobiliários.

## Tarefas

### Estruturar banco de dados
A primeira tarefa é criar um banco PostgreSQL na [AWS](https://aws.amazon.com/pt/free).

Criar uma tabela `fund_report` onde serão salvas as cotas de cada fundo dia a dia, com a seguinte estrutura:

```
{
  cnpj varchar(14)
  quote_value float(8) not null
  date_report date not null
}
```

### Crawler dos dados

Desenvolver um crawler do seguinte link da CVM: 
http://dados.cvm.gov.br/dados/FI/DOC/INF_DIARIO/DADOS/inf_diario_fi_{SCRAP_DATE}.csv

Onde:

- `{SCRAP_DATE}` = Exemplo: para Janeiro de 2021 (01/2021), ficaria `202101` (Sempre no formato YYYYMM).

O link vai baixar um arquivo CSV mensal com as cotas de todos os fundos, todos os dias do mês. Você, então, deverá salvar os campos `CNPJ_FUNDO`, `VL_QUOTA` e `DT_COMPTC` na tabela que fora criada acima.

**A base deverá ser populada com os dados do ano de 2021 (de Janeiro a Dezembro).**

### API dos dados de rentabilidade

O próximo passo será criar uma API Rest que seja responsável por retornar a rentabilidade de um fundo específico:

https://localhost:3000/funds/{CNPJ}/rentability?init_date={INIT_DATE}&end_date={END_DATE}
- `{CNPJ}` = Cnpj do fundo sem traços, pontos e barras (. - /)
- `{INIT_DATE}` = Data inicial no formato **YYYY-MM-DD**
- `{END_DATE}` = Data final no formato **YYYY-MM-DD**

O retorno um **JSON** com a rentabilidade do fundo no período, caso não seja passado nenhuma data, calcular o período completo.

```
{
  "rentability": Float
}
```

#### Como calcular a rentabilidade

1. Primeiro deve se calcular o Fator: `fator = (cota_final / cota_inicial)`
2. A rentabilidade se dá por `r = (f - 1) * 100`

<hr />

_As tarefas abaixo não são obrigatórias, avaliaremos como um extra._

## Bônus 1 

Adicionar um parâmetro na API, `"invest_value"` que seria o **patrimônio** na `INIT_DATE`
e retornar quanto seria o patrimônio no `END_DATE`.

```
  {
    "rentability": Float,
    "equity_value": Float
  }
```

## Bônus 2

Adicionar o parâmetro `return=full` na API que retorna uma lista com a posição **diária** do investimento no fundo.

Por exemplo:

- `init_date` = 2021-01-04
- `end_date` = 2021-01-08
- `invest_value` = 10000
- `cnpj` = 0000000000
- `return` = full

O retorno deveria ser:

```
[
  {
    "date_report": "2021-01-04",
    "rentability": 0,
    "equity_value": 10000
  },
  ...,
  {
    "date_report": "2021-01-08",
    "rentability": 0.1, // Rentabilidade no dia
    "equity_value": 11000 // Patrimônio no dia
  }
]
```

## O que será avaliado no teste

- Extração dos dados
- Manipulação dos arquivos
- Manipulação de listas e dicionários
- Noção de banco de dados
- Noção de criação de uma API
- Componentização das funções por cada responsabilidade (ETL - Extract, Transform and Load)
- Organização da code base
