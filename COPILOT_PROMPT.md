# PROMPT PARA O COPILOT — RETAIL SALES ANALYTICS

Quero que você construa um relatório profissional no Power BI usando os seis arquivos CSV fornecidos:

- fVendas.csv
- fMetas.csv
- dClientes.csv
- dProdutos.csv
- dLojas.csv
- dCanal.csv

O projeto se chama **Retail Sales Analytics — Power BI** e será usado em um portfólio profissional para vagas de Analista de Dados / BI.

## 1. Power Query — limpeza e preparação

Faça as transformações abaixo antes de criar o modelo.

### fVendas
- Defina VendaID, ClienteID, ProdutoID, LojaID, CanalID e Quantidade como números inteiros.
- Defina Data como data.
- Defina PrecoUnitario, CustoUnitario e Desconto como números decimais.
- Remova duplicatas utilizando VendaID.
- Substitua valores nulos de Desconto por 0.
- Não crie Receita ou Lucro como colunas físicas; quero esses cálculos como medidas DAX.

### dClientes
- Aplique Trim e Clean nos campos de texto.
- Padronize Regiao para: Sudeste, Sul, Nordeste, Centro-Oeste e Norte.
- Defina DataCadastro como data.
- Garanta uma única linha por ClienteID.

### dProdutos
- Aplique Trim e Clean em Produto, Categoria, Subcategoria e Marca.
- Padronize Categoria.
- Defina PrecoBase e CustoBase como decimais.
- Garanta uma única linha por ProdutoID.

### dLojas e dCanal
- Aplique Trim e Clean aos textos.
- Defina as chaves como inteiros.
- Mantenha uma única linha por chave.

### fMetas
- Data como data.
- LojaID como inteiro.
- MetaReceita e MetaLucro como decimal/moeda.

## 2. Modelo de dados

Monte um modelo estrela, evitando relacionamentos muitos-para-muitos.

Crie uma tabela calendário chamada `dCalendario`, cobrindo da menor até a maior data de fVendas.

Inclua:
- Ano
- MesNumero
- Mes
- AnoMes
- Trimestre
- DiaSemanaNumero
- DiaSemana

Marque dCalendario como tabela de datas e ordene Mes por MesNumero.

Relacione:

- dCalendario[Date] 1:* fVendas[Data]
- dClientes[ClienteID] 1:* fVendas[ClienteID]
- dProdutos[ProdutoID] 1:* fVendas[ProdutoID]
- dLojas[LojaID] 1:* fVendas[LojaID]
- dCanal[CanalID] 1:* fVendas[CanalID]
- dCalendario[Date] 1:* fMetas[Data]
- dLojas[LojaID] 1:* fMetas[LojaID]

Use filtro em uma única direção, das dimensões para as fatos.

## 3. Medidas DAX

Crie uma tabela chamada `_Medidas` e adicione:

Receita Bruta =
SUMX(
    fVendas,
    fVendas[Quantidade] * fVendas[PrecoUnitario]
)

Receita Total =
SUMX(
    fVendas,
    fVendas[Quantidade] *
    fVendas[PrecoUnitario] *
    (1 - fVendas[Desconto])
)

Custo Total =
SUMX(
    fVendas,
    fVendas[Quantidade] * fVendas[CustoUnitario]
)

Lucro Total = [Receita Total] - [Custo Total]

Margem % = DIVIDE([Lucro Total], [Receita Total])

Quantidade Vendida = SUM(fVendas[Quantidade])

Total Pedidos = DISTINCTCOUNT(fVendas[PedidoID])

Ticket Médio = DIVIDE([Receita Total], [Total Pedidos])

Clientes Ativos = DISTINCTCOUNT(fVendas[ClienteID])

Meta Receita = SUM(fMetas[MetaReceita])

Meta Lucro = SUM(fMetas[MetaLucro])

Atingimento Meta % = DIVIDE([Receita Total], [Meta Receita])

Diferença Meta = [Receita Total] - [Meta Receita]

Receita Mês Anterior =
CALCULATE(
    [Receita Total],
    DATEADD(dCalendario[Date], -1, MONTH)
)

Crescimento MoM % =
DIVIDE(
    [Receita Total] - [Receita Mês Anterior],
    [Receita Mês Anterior]
)

Receita Ano Anterior =
CALCULATE(
    [Receita Total],
    SAMEPERIODLASTYEAR(dCalendario[Date])
)

Crescimento YoY % =
DIVIDE(
    [Receita Total] - [Receita Ano Anterior],
    [Receita Ano Anterior]
)

Receita YTD =
TOTALYTD(
    [Receita Total],
    dCalendario[Date]
)

Lucro YTD =
TOTALYTD(
    [Lucro Total],
    dCalendario[Date]
)

Formate valores monetários em Real brasileiro, percentuais com 1 ou 2 casas e números inteiros com separador de milhar.

## 4. Design

Quero visual moderno, profissional e consistente com portfólio de tecnologia.

Paleta:
- Fundo principal: #0B1020
- Cards/painéis: #151A2E
- Roxo principal: #7C3AED
- Ciano de destaque: #22D3EE
- Texto principal: #F8FAFC
- Positivo: #22C55E
- Alerta: #F59E0B
- Negativo: #EF4444

Use bom espaçamento, alinhamento consistente, bordas discretas e evite poluição visual.
Mantenha o relatório em 16:9.
Crie navegação por botões entre páginas.
Use títulos claros e pequenos textos de contexto.
Evite gráficos 3D.

## 5. Página 1 — Visão Geral

Título: **Visão Geral Executiva**

Cards:
- Receita Total
- Lucro Total
- Margem %
- Ticket Médio
- Total Pedidos
- Crescimento YoY %

Visuais:
- Gráfico de linhas: Receita Total por AnoMes.
- Barras horizontais: Receita Total por Categoria.
- Barras: Receita Total por Região.
- Rosca ou barras: Receita Total por Canal.
- Colunas agrupadas ou combinação: Receita Total x Meta Receita por AnoMes.

Segmentadores:
- Ano
- Mês
- Região
- Categoria
- Canal

Adicione um indicador visual para Atingimento Meta %.

## 6. Página 2 — Produtos & Categorias

Título: **Performance de Produtos**

Cards:
- Receita Total
- Lucro Total
- Margem %
- Quantidade Vendida

Visuais:
- Top 10 Produtos por Receita Total.
- Top 10 Produtos por Lucro Total.
- Receita Total e Lucro Total por Categoria.
- Margem % por Categoria.
- Matriz com Produto, Categoria, Receita Total, Lucro Total, Margem %, Quantidade Vendida.
- Use formatação condicional na matriz.

Segmentadores:
- Ano
- Categoria
- Marca
- Canal

## 7. Página 3 — Clientes & Regiões

Título: **Clientes & Mercado**

Cards:
- Clientes Ativos
- Ticket Médio
- Receita Total
- Total Pedidos

Visuais:
- Receita por Região.
- Receita por Estado.
- Top 10 Clientes por Receita.
- Ticket Médio por Região.
- Distribuição de Clientes por FaixaEtaria.
- Receita por Canal.

Se um mapa geográfico funcionar corretamente, use Estado como localização; caso contrário, use gráfico de barras.

Segmentadores:
- Ano
- Região
- Estado
- FaixaEtaria
- Canal

## 8. Página 4 — Performance & Metas

Título: **Performance Comercial & Metas**

Cards:
- Meta Receita
- Receita Total
- Atingimento Meta %
- Diferença Meta

Visuais:
- Receita Total x Meta Receita por AnoMes.
- Atingimento Meta % por Loja.
- Ranking de lojas por Receita Total.
- Ranking de lojas por Lucro Total.
- Matriz com Loja, Receita Total, Meta Receita, Atingimento Meta %, Diferença Meta e Lucro Total.
- Formatação condicional:
  - verde para atingimento >= 100%;
  - amarelo entre 90% e 99,99%;
  - vermelho abaixo de 90%.

Segmentadores:
- Ano
- Mês
- Região
- Loja

## 9. Interatividade

- Configure as interações de forma coerente entre os visuais.
- Adicione tooltips úteis.
- Permita drill-through de Categoria para Produto e de Região para Loja, se possível.
- Crie botões para limpar filtros.
- Crie botões de navegação.
- Use bookmarks apenas se melhorarem a experiência.

## 10. Storytelling e insights

Não crie apenas gráficos. Estruture o relatório para responder:
- Como a receita evolui no tempo?
- Qual o crescimento de 2025 em relação a 2024?
- Quais categorias e produtos mais contribuem para receita e lucro?
- Quais regiões lideram?
- Qual é a evolução da participação dos canais digitais?
- Quais lojas estão acima ou abaixo da meta?
- Onde existem oportunidades de melhoria de margem?

Inclua uma pequena caixa de texto em cada página explicando em 1–2 frases o objetivo daquela análise.

## 11. Resultado final

O resultado deve parecer um dashboard corporativo de portfólio, pronto para ser apresentado em processo seletivo para estágio/júnior em Dados e BI.

Não invente campos que não existam nos arquivos. Se alguma funcionalidade não puder ser criada automaticamente, explique exatamente o passo manual que devo fazer no Power BI.
