# Retail Sales Analytics — Project Specification

Este documento resume os requisitos funcionais e analíticos definidos para o projeto **Retail Sales Analytics — Power BI**.

## Objetivo

Construir uma solução de Business Intelligence para acompanhar desempenho comercial, receita, lucro, margem, clientes, produtos, canais e metas.

## Dados

O projeto utiliza seis arquivos de origem:

- `fVendas.csv`
- `fMetas.csv`
- `dClientes.csv`
- `dProdutos.csv`
- `dLojas.csv`
- `dCanal.csv`

## Preparação

Principais regras de qualidade e transformação:

- tipagem correta de chaves, datas e valores;
- remoção de duplicidades em vendas;
- tratamento de valores nulos;
- padronização de textos;
- garantia de unicidade nas dimensões;
- criação de calendário analítico.

## Modelagem

Modelo dimensional em esquema estrela, com:

- `fVendas`
- `fMetas`
- `dClientes`
- `dProdutos`
- `dLojas`
- `dCanal`
- `dCalendario`

Os relacionamentos usam direção de filtro das dimensões para as tabelas fato.

## KPIs

O relatório acompanha, entre outros:

- Receita Total
- Lucro Total
- Margem %
- Quantidade Vendida
- Total de Pedidos
- Ticket Médio
- Clientes Ativos
- Meta de Receita
- Meta de Lucro
- Atingimento de Meta %
- Crescimento MoM %
- Crescimento YoY %
- Receita YTD
- Lucro YTD

## Páginas do dashboard

### 1. Visão Geral Executiva
Evolução temporal, receita, lucro, margem, categorias, regiões, canais e metas.

### 2. Produtos & Categorias
Performance por produto, categoria e marca.

### 3. Clientes & Mercado
Clientes, regiões, estados, canais e ticket médio.

### 4. Performance Comercial & Metas
Comparação entre realizado e meta por loja e período.

## Design

O dashboard foi planejado com visual escuro, hierarquia clara, foco em KPIs e baixa poluição visual. A navegação e os filtros foram desenhados para facilitar exploração por diferentes dimensões do negócio.

## Resultado esperado

Uma solução de BI versionável e documentada, adequada para demonstrar competências em **Power BI, Power Query, DAX, modelagem dimensional, qualidade de dados, análise de KPIs e storytelling com dados**.
