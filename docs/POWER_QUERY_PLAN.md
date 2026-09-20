# Plano de Tratamento — Power Query

Execute estas etapas antes da modelagem:

## fVendas
1. Definir tipos:
   - IDs e Quantidade: número inteiro.
   - PrecoUnitario, CustoUnitario e Desconto: número decimal.
   - Data: data.
2. Remover duplicatas usando `VendaID`.
3. Substituir valores nulos de `Desconto` por `0`.
4. Validar que Quantidade > 0 e preços/custos >= 0.
5. Não criar Receita/Lucro no Power Query; deixe os cálculos financeiros como medidas DAX.

## dClientes
1. Aplicar Trim e Clean nos campos textuais.
2. Padronizar `Regiao` para capitalização consistente:
   Sudeste, Sul, Nordeste, Centro-Oeste e Norte.
3. Definir DataCadastro como data.
4. Garantir unicidade de ClienteID.

## dProdutos
1. Trim/Clean em Produto, Categoria, Subcategoria e Marca.
2. Padronizar Categoria.
3. Tipar PrecoBase e CustoBase como decimal.
4. Garantir unicidade de ProdutoID.

## dLojas e dCanal
1. Trim/Clean nos textos.
2. Definir IDs como inteiros.
3. Garantir unicidade das chaves.

## fMetas
1. Data como data.
2. LojaID como inteiro.
3. MetaReceita e MetaLucro como decimal/moeda.
