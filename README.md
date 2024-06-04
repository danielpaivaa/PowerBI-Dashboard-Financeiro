# Criando um Dashboard Financeiro em Power BI

## Introdução

Estou criando um dashboard financeiro a partir de um conjunto de dados fictício. Este dashboard oferece insights sobre a receita, despesa, impostos, lucro, margens, transações e fluxo de caixa da empresa.

## Passo a Passo para Criar o Dashboard

### Criando um plano de fundo
  - Plano de fundo criado utilizando Microsoft PowerPoint

![Painel Financeiro](arquivos/Plano%20de%20Fundo.png)

### Importação e Transformação dos Dados

- **Passos de Transformação:**
  - **Remoção de dados nulos:** As colunas e linhas nulas foram removidas da base de dados.
  - **Alteração dos tipos de dados:** Após verificação, observou-se que os tipos de dados não correspondiam ao desejado e, assim, foi feita a alteração.

- **Criando novas medidas com DAX:**
  - **Receita:** Medida criada a partir da soma da coluna `Valor da Movimentação` para transações do tipo `Recebimento`.
    > *Receita = CALCULATE(SUM('Movimentações'[Valor da Movimentação]), 'Movimentações'[Tipo] == "Recebimento")*
  - **Despesa:** Medida criada a partir da soma da coluna `Valor da Movimentação` para transações do tipo `Despesa`.
    > *Despesas = -CALCULATE(SUM('Movimentações'[Valor da Movimentação]), 'Movimentações'[Tipo] == "Pagamento")*
  - **Imposto:** Medida criada a partir da medida `Receita` multiplicada por um valor fictício.
    > *Impostos = [Receita] * 0.15*
  - **Lucro:** Medida criada a partir do cálculo entre as medidas: `Receita`, `Despesa` e `Imposto`.
    > *Lucro = [Receita] - [Despesas] - [Impostos]*
  - **Margem:** Medida criada a partir do cálculo entre as medidas: `Lucro` e `Receita`.
    > *Margem = [Lucro] / [Receita]*
  - **Transações via PIX:** Medida criada a partir da soma da coluna `Forma Pagamento` para transações de forma de pagamento `PIX`.
    > *Transações PIX = CALCULATE(COUNTROWS('Movimentações'), 'Movimentações'[Forma Pagamento] == "PIX")*

## Interpretação dos Insights

## Dashboard
![Painel Financeiro](arquivos/Aula%204.png)

### Receita, Despesa, Imposto e Lucro
- **Receita**: A empresa gerou uma receita total de R$ 94,60 milhões, demonstrando uma forte capacidade de geração de receita ao longo do período analisado.

- **Despesa**: As despesas totalizaram R$ 44,86 milhões, o que representa uma gestão cuidadosa dos custos operacionais e outras despesas.

- **Imposto**: O valor dos impostos foi de R$ 14,19 milhões, indicando uma significativa contribuição tributária.

- **Lucro**: O lucro líquido ficou em R$ 35,55 milhões, refletindo a rentabilidade da empresa após a dedução de todas as despesas e impostos.

### Margem de Lucro
- **Margem**: A margem de lucro foi de 37,58%, um indicativo positivo da eficiência da empresa em controlar seus custos em relação à receita gerada.

### Transações
- **Total de Transações**: Foram realizadas um total de R$ 2,73 mil transações, mostrando um volume significativo de atividade financeira.
- **Transações via PIX**: Destas, R$ 1,20 mil foram realizadas via PIX, representando 44,04% do total das transações, o que destaca a popularidade e a conveniência do uso do PIX como forma de pagamento.

### Fluxo de Caixa
- **Consideração Geral**: O fluxo de caixa ao longo do ano apresentou variações, com meses de aumento e outros de diminuição. No entanto, o saldo final foi positivo, totalizando R$ 36 milhões. Isso reflete uma gestão eficaz das entradas e saídas de caixa, garantindo a saúde financeira da empresa.

## Considerações sobre a Base de Dados

A base de dados utilizada contém as seguintes colunas:

- **Número Movimentação:** Identificação da transação.
- **Nome:** Nome do cliente ou fornecedor.
- **Tipo Pessoa:** Tipo de pessoa (Física ou Jurídica).
- **Município:** Cidade onde a transação ocorreu.
- **Data da Movimentação:** Data da transação.
- **Valor da Movimentação:** Valor da transação.
- **Tipo:** Tipo da transação (Receita, Despesa, Imposto).
- **Banco:** Banco utilizado na transação.
- **Imagem:** Link para os ícones dos bancos.
- **Forma Pagamento:** Forma de pagamento utilizada (PIX, Boleto, Cartão, etc.).
