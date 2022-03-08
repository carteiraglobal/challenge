<img src="https://img.carteiraglobal.com/logo-cg.png" alt="logo-cg" style="zoom:50%;float:left;" />

# Challenge Backend

## Objetivos

O objetivo desse Challenge é testar a sua capacidade e criatividade para extrair, transformar e carregar as informações limpas de um site em uma base de dados.

Iremos trabalhar com os dados abertos da CVM - Comissão de Valores Mobiliários.

## Regras de Negócio:

A primeira tarefa é criar um banco postgresql na [AWS](https://aws.amazon.com/pt/free).

Criar uma tabela `fund_report` onde serão salvas as cotas de cada fundo dia a dia, com a seguinte estrutura:

```
{
  cnpj varchar(14)
  quote_value float(8) not null
  date_report date not null
}
```

Então deverá criar um crawler no link da CVM
http://dados.cvm.gov.br/dados/FI/DOC/INF_DIARIO/DADOS/inf_diario_fi_{SCRAP_DATE}.csv

Onde:

- `SCRAP_DATE` = Exemplo: para Janeiro de 2021 (01/2021), ficaria `202101` (Sempre no formato YYYYMM).<p>
  O link vai baixar um arquivo .csv mensal com as cotas de todos os fundos, todos os dias do mês.
  Você, então, deverá salvar os campos `CNPJ_FUNDO`, `VL_QUOTA` e `DT_COMPTC` na tabela que fora criada acima.</p>

**A base deverá ser populada com os dados do ano de 2021 (de Janeiro a Dezembro).**
<br/>

O próximo passo será criar uma API Rest que receba os seguintes parametros:

- `{CNPJ}` = Cnpj do fundo sem traços, pontos e barras (. - /)
- `{INIT_DATE}` = Data inicial no formato **YYYY-MM-DD**
- `{END_DATE}` = Data final no formato **YYYY-MM-DD**

E retornar um **JSON** com a rentabilidade do fundo no período, caso não seja passado nenhuma data, calcular o período completo.

```json
{
  "rentability": Float
}
```

### Calcular a rentabilidade:

1. Primeiro deve se calcular o Fator: `fator = (cota_final / cota_inicial)`
2. A rentabilidade se dá por `r = (f - 1) * 100`

## _Você deverá disponibilizar a URL da API no README do challenge no GitHub_

<hr /><br />

## Bônus 1 _(não é obrigatório, avaliaremos como um extra)_

Adicionar um parâmetro na API, `"invest_value"` que seria o **patrimônio** na `INIT_DATE`
e retornar quanto seria o patrimônio no `END_DATE`.

```json
  {
    "rentability": Float,
    "equity_value": Float
  }
```

## Bônus 2 _(não é obrigatório, avaliaremos como um extra)_

Adicionar o parâmetro `return=full` na API que retorna uma lista com a posição **diária** do investimento no fundo.

Por exemplo:

- `init_date` = 2021-01-04
- `end_date` = 2021-01-08
- `invest_value` = 10000
- `cnpj` = 0000000000
- `return` = full

O retorno deveria ser:

```json
[
  {
    "date_report": "2021-01-04",
    "rentability": 0,
    "equity_value": 10000
  },
  ...,
  {
    "date_report": "2021-01-08",
    "rentability": Rentabilidade no dia,
    "equity_value": Patrimônio no dia
  }
]
```

## O que será avaliado

- Extração dos dados;
- Manipulação dos arquivos;
- Manipulação de listas e dicionários;
- Noção de banco de dados;
- Noção de criação de uma API simples;
- Componentização das funções por cada responsabilidade (extract, transform, load);
- Organização de code base;
