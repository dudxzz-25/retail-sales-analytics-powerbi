# Dicionário de Dados

## fVendas
| Coluna | Descrição |
|---|---|
| VendaID | Identificador único da linha de venda. Use para remover duplicatas. |
| PedidoID | Identificador do pedido. Um pedido pode ter várias linhas. |
| Data | Data da venda. |
| ClienteID | Chave para dClientes. |
| ProdutoID | Chave para dProdutos. |
| LojaID | Chave para dLojas. |
| CanalID | Chave para dCanal. |
| Quantidade | Quantidade do item. |
| PrecoUnitario | Preço unitário praticado na venda. |
| CustoUnitario | Custo unitário estimado. |
| Desconto | Percentual de desconto em formato decimal. Há alguns nulos intencionais. |

## fMetas
| Coluna | Descrição |
|---|---|
| Data | Primeiro dia do mês da meta. |
| LojaID | Chave da loja. |
| MetaReceita | Meta mensal de receita da loja. |
| MetaLucro | Meta mensal indicativa de lucro. |

## dClientes
ClienteID, NomeCliente, Sexo, Idade, FaixaEtaria, Cidade, Estado, Regiao e DataCadastro.

## dProdutos
ProdutoID, Produto, Categoria, Subcategoria, Marca, PrecoBase e CustoBase.

## dLojas
LojaID, Loja, Cidade, Estado e Regiao.

## dCanal
CanalID e Canal.
