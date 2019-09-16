<img src="https://img.carteiraglobal.com/logo-cg.png" alt="logo-cg" style="zoom:50%;float:left;" />

# Challenge Frontend

## Objetivos
Desenvolver uma calculadora de Simuladora de Renda Fixa utilizando style guide e regras de negócio abaixo.
- O usuário deverá ser capaz de alterar o resultado apresentado no gráfico, utilizando os Sliders à esquerda;
- O app deverá fazer uma requisição http para o endpoint das configurações dos Sliders e salvá-las na Store.

      Endpoint:
      GET: https://carbon.carteiraglobal.com/

Exemplo Formato da response da http request:

    {
        minInvestValue: 0,
        maxInvestValue: 999999,
        minPeriod: 1,
        maxPeriod: 36,
        minCdbLcAnualTax: 0,
        maxCdbLcAnualTax: 110,
        minLciLcaAnualTax: 0,
        maxLciLcaAnualTax: 135,
        minDiTax: 0,
        maxDiTax: 18,
        minIpcaTax: 0,
        maxIpcaTax: 18,
    }

## Regras de Negócio
*Aqui estarão definas as fórmulas de regras de negócio*

## Requisitos Técnicos
- O seu código deverá ser compartilhado em um reposítório público no Github;
- Você deverá usar React e Redux;
- Você poderá usar scaffolds como Create React App, ou framework de componentes como Ant Design ou Materialize, desde que se atente ao que será avaliado.

## O que será avaliado
- Componetização, ou seja, capacidade de reutilização de estilo e comportamento dos componentes;
- Organização de code base, tanto código quanto arquivos;
- Mobile UX.
