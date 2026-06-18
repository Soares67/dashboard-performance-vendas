# Dados do Projeto

Esta pasta contém os arquivos usados como fonte de dados do dashboard **Dashboard Performance Vendas**.

Os dados são fictícios e foram criados para simular uma operação comercial de uma empresa de hardware e produtos de escritório.

---

## Estrutura da pasta

Os arquivos foram separados em duas pastas principais:

```text
data/
├── apoio/
└── vendas/
```

---

## Pasta `vendas/`

A pasta `vendas/` contém os arquivos anuais de vendas.

```text
vendas/
├── Vendas 2020.csv
├── Vendas 2021.csv
├── Vendas 2022.csv
├── Vendas 2023.csv
└── Vendas 2024.csv
```

Esses arquivos são carregados pelo Power Query a partir da pasta.

A regra usada no tratamento foi:

1. buscar todos os arquivos da pasta;
2. filtrar somente os arquivos de vendas;
3. transformar os arquivos;
4. combinar tudo em uma única tabela de vendas.

Esse processo permite atualizar o dashboard adicionando novos arquivos de vendas na mesma pasta, desde que eles mantenham a mesma estrutura de colunas.

---

## Pasta `apoio/`

A pasta `apoio/` contém tabelas auxiliares usadas no modelo.

```text
apoio/
├── Clientes.csv
├── Funil.xlsx
├── Imgs Vendedores.xlsx
├── Leads.xlsx
├── Metas.csv
├── Produtos.csv
└── Vendedores.csv
```

Esses arquivos complementam a tabela de vendas e permitem criar análises por cliente, vendedor, produto, meta e funil de leads.

---

## Descrição dos arquivos

### `Clientes.csv`

Base de clientes usada para relacionar as vendas e os leads aos clientes cadastrados.

### `Produtos.csv`

Cadastro de produtos vendidos pela empresa.

Essa base permite analisar o faturamento por diferentes níveis, como:

```text
Categoria → Subcategoria → Marca → Produto
```

### `Vendedores.csv`

Cadastro dos vendedores usados nas análises de desempenho comercial.

Essa tabela é usada no ranking de vendedores, nos filtros e nos gráficos da página de desempenho.

### `Imgs Vendedores.xlsx`

Arquivo com as imagens dos vendedores usadas no dashboard.

As imagens são fictícias e foram usadas apenas para fins visuais.

### `Metas.csv`

Tabela com as metas mensais de cada vendedor em todos os anos da base.

Ela é usada para calcular o percentual de meta atingida.

### `Leads.xlsx`

Base de leads usada na página de conversão.

Essa tabela permite calcular indicadores como:

* total de leads;
* leads convertidos;
* leads perdidos;
* taxa de conversão;
* taxa de perda;
* tempo médio de conversão.

### `Funil.xlsx`

Tabela usada para organizar as etapas do funil de vendas.

As etapas consideradas no dashboard foram:

```text
Contato Inicial
Qualificação
Apresentação
Proposta
Fechamento
```

---

## Observações sobre os dados

Todos os dados deste projeto são fictícios.

Isso inclui:

* nomes de vendedores;
* fotos dos vendedores;
* clientes;
* produtos;
* vendas;
* metas;
* leads;
* etapas do funil.

As fotos e nomes dos vendedores foram gerados com IA e usados apenas para deixar o dashboard mais próximo de um cenário real.

---

## Atualização dos dados

O principal ponto da estrutura de dados é permitir que a tabela de vendas seja atualizada de forma simples.

Para adicionar um novo ano de vendas, basta incluir um novo arquivo na pasta `vendas/`, seguindo o mesmo padrão dos arquivos existentes.

Exemplo:

```text
Vendas 2025.csv
```

Ao atualizar o Power BI, o Power Query deve reconhecer o novo arquivo, aplicar os mesmos tratamentos e incluir os dados na tabela consolidada de vendas.

---

## Importante

Caso os nomes das pastas ou arquivos sejam alterados, pode ser necessário ajustar a origem dos dados no Power Query.

Por isso, a estrutura da pasta `data/` deve ser mantida para que o dashboard continue funcionando corretamente.
