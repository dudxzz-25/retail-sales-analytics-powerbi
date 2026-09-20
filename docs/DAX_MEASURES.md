# Medidas DAX

Crie uma tabela vazia chamada `_Medidas` e armazene nela as medidas.

```DAX
Receita Bruta =
SUMX(
    fVendas,
    fVendas[Quantidade] * fVendas[PrecoUnitario]
)
```

```DAX
Receita Total =
SUMX(
    fVendas,
    fVendas[Quantidade] *
    fVendas[PrecoUnitario] *
    (1 - fVendas[Desconto])
)
```

```DAX
Custo Total =
SUMX(
    fVendas,
    fVendas[Quantidade] * fVendas[CustoUnitario]
)
```

```DAX
Lucro Total = [Receita Total] - [Custo Total]
```

```DAX
Margem % = DIVIDE([Lucro Total], [Receita Total])
```

```DAX
Quantidade Vendida = SUM(fVendas[Quantidade])
```

```DAX
Total Pedidos = DISTINCTCOUNT(fVendas[PedidoID])
```

```DAX
Ticket Médio = DIVIDE([Receita Total], [Total Pedidos])
```

```DAX
Clientes Ativos = DISTINCTCOUNT(fVendas[ClienteID])
```

```DAX
Meta Receita = SUM(fMetas[MetaReceita])
```

```DAX
Meta Lucro = SUM(fMetas[MetaLucro])
```

```DAX
Atingimento Meta % = DIVIDE([Receita Total], [Meta Receita])
```

```DAX
Diferença Meta = [Receita Total] - [Meta Receita]
```

```DAX
Receita Mês Anterior =
CALCULATE(
    [Receita Total],
    DATEADD(dCalendario[Date], -1, MONTH)
)
```

```DAX
Crescimento MoM % =
DIVIDE(
    [Receita Total] - [Receita Mês Anterior],
    [Receita Mês Anterior]
)
```

```DAX
Receita Ano Anterior =
CALCULATE(
    [Receita Total],
    SAMEPERIODLASTYEAR(dCalendario[Date])
)
```

```DAX
Crescimento YoY % =
DIVIDE(
    [Receita Total] - [Receita Ano Anterior],
    [Receita Ano Anterior]
)
```

```DAX
Receita YTD =
TOTALYTD(
    [Receita Total],
    dCalendario[Date]
)
```

```DAX
Lucro YTD =
TOTALYTD(
    [Lucro Total],
    dCalendario[Date]
)
```
