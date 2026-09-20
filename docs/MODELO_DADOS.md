# Modelo de Dados

```text
                         dCalendario
                       /             \
                      /               \
                 fVendas             fMetas
                /   |   \               |
               /    |    \              |
      dClientes dProdutos dCanal       dLojas
                 \          /
                  \        /
                    dLojas
```

## Relacionamentos
- dCalendario[Date] 1:* fVendas[Data]
- dClientes[ClienteID] 1:* fVendas[ClienteID]
- dProdutos[ProdutoID] 1:* fVendas[ProdutoID]
- dLojas[LojaID] 1:* fVendas[LojaID]
- dCanal[CanalID] 1:* fVendas[CanalID]
- dCalendario[Date] 1:* fMetas[Data]
- dLojas[LojaID] 1:* fMetas[LojaID]

Use direção de filtro única das dimensões para as tabelas fato.
