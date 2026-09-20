# Retail Sales Analytics — Power BI

Projeto de portfólio de Business Intelligence com dados sintéticos de varejo.

## Objetivo
Construir uma solução de BI para acompanhar receita, lucro, margem, pedidos, ticket médio, clientes, produtos, canais, regiões e atingimento de metas.

## Arquivos de dados
- `data/raw/fVendas.csv`: fato de vendas, em nível de item do pedido.
- `data/raw/fMetas.csv`: metas mensais por loja.
- `data/raw/dClientes.csv`: dimensão de clientes.
- `data/raw/dProdutos.csv`: dimensão de produtos.
- `data/raw/dLojas.csv`: dimensão de lojas.
- `data/raw/dCanal.csv`: dimensão de canais.

## Volume
- 15,513 linhas no arquivo bruto de vendas.
- 15,485 linhas válidas antes das duplicatas intencionais.
- 2,500 clientes sintéticos.
- 120 produtos.
- 12 lojas.
- 4 canais.
- 288 registros mensais de metas.

## Qualidade dos dados
Algumas imperfeições foram inseridas de propósito para demonstrar tratamento no Power Query:
- duplicatas em `fVendas`, identificadas por `VendaID`;
- valores nulos em `Desconto`;
- variações de maiúsculas/minúsculas e espaços em alguns campos textuais de dimensões.

Esses problemas devem ser tratados antes da modelagem.

## Modelo recomendado
Modelo estrela com:
- `fVendas`
- `fMetas`
- `dClientes`
- `dProdutos`
- `dLojas`
- `dCanal`
- `dCalendario` criada no Power BI.

## Páginas do relatório
1. Visão Geral
2. Produtos & Categorias
3. Clientes & Regiões
4. Performance & Metas

## Tecnologias
Power BI · Power Query · DAX · Modelagem Dimensional · GitHub

## Observação
Todos os dados deste projeto são sintéticos e foram criados exclusivamente para fins educacionais e de portfólio.
