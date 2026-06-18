# Tratamento dos Dados

Este documento resume como os dados foram tratados no Power Query antes de serem usados no dashboard **Dashboard Performance Vendas**.

O objetivo do tratamento foi criar um fluxo simples de atualização: quando novos arquivos de vendas forem adicionados à pasta, o Power BI consegue carregar esses dados e atualizar o relatório seguindo a mesma estrutura.

---

## Origem dos dados

Os dados do projeto estão organizados na pasta `data/`, separada em duas partes:

```text
data/
├── apoio/
└── vendas/
```

A pasta `vendas/` contém os arquivos anuais de vendas.

A pasta `apoio/` contém tabelas auxiliares, como clientes, produtos, vendedores, metas, leads, funil e imagens dos vendedores.

---

## Tratamento da tabela de vendas

A tabela de vendas foi criada a partir dos arquivos da pasta `data/vendas`.

O fluxo usado no Power Query foi:

```text
1. Buscar todos os arquivos da pasta
2. Filtrar somente os arquivos de vendas
3. Transformar os arquivos encontrados
4. Padronizar as colunas
5. Combinar tudo em uma tabela única
6. Ajustar tipos de dados
7. Carregar a tabela final no modelo
```

Essa etapa permite que o dashboard seja atualizado com novos arquivos de vendas, desde que eles mantenham o mesmo padrão de colunas.

Exemplo:

```text
data/vendas/
├── Vendas 2020.csv
├── Vendas 2021.csv
├── Vendas 2022.csv
├── Vendas 2023.csv
└── Vendas 2024.csv
```

Se um novo arquivo como `Vendas 2025.csv` for adicionado com a mesma estrutura, ele pode ser incorporado ao modelo na próxima atualização.

---

## Tabelas de apoio

As tabelas auxiliares foram carregadas separadamente.

Arquivos usados:

```text
data/apoio/
├── Clientes.csv
├── Funil.xlsx
├── Imgs Vendedores.xlsx
├── Leads.xlsx
├── Metas.csv
├── Produtos.csv
└── Vendedores.csv
```

Essas tabelas complementam a tabela de vendas e permitem análises por cliente, produto, vendedor, metas e funil de leads.

---

## Clientes

A tabela de clientes foi usada para relacionar as vendas e os leads aos clientes cadastrados.

Ela permite analisar a base comercial a partir dos clientes envolvidos nas vendas e no processo de conversão.

---

## Produtos

A tabela de produtos foi usada para enriquecer a análise de vendas.

Ela permite navegar pelo faturamento em diferentes níveis:

```text
Categoria → Subcategoria → Marca → Produto
```

Essa hierarquia foi usada no gráfico de faturamento por categoria, permitindo análise com drill down.

---

## Vendedores

A tabela de vendedores foi usada para criar as análises de desempenho comercial.

Ela é usada em:

* ranking de vendedores;
* filtros;
* gráficos de desempenho;
* tooltip personalizado de vendedor;
* comparação entre volume de vendas e ticket médio.

---

## Imagens dos vendedores

O arquivo de imagens foi usado apenas para fins visuais no dashboard.

As imagens são fictícias e foram associadas aos vendedores para deixar a página de desempenho mais próxima de um relatório comercial real.

---

## Metas

A tabela de metas possui a meta mensal de cada vendedor em todos os anos da base.

Ela foi usada para calcular o percentual de meta atingida.

```text
Meta Atingida = Faturamento Total / Meta
```

Essa métrica aparece tanto na visão geral quanto na análise individual dos vendedores.

---

## Leads

A tabela de leads foi usada na página de conversão.

A partir dela foram criadas métricas como:

* total de leads;
* leads convertidos;
* leads perdidos;
* taxa de conversão;
* taxa de perda;
* tempo médio de conversão.

O tempo médio considera a diferença entre a data de criação do lead e a data de conversão.

---

## Funil

A tabela de funil foi usada para organizar as etapas do processo comercial.

As etapas consideradas foram:

```text
Contato Inicial
Qualificação
Apresentação
Proposta
Fechamento
```

O funil mostra em qual etapa cada lead parou, ajudando a visualizar onde ocorrem mais perdas no processo comercial.

---

## Padronização dos dados

Durante o tratamento, os principais ajustes foram:

* definição dos tipos de dados;
* padronização de colunas;
* combinação dos arquivos de vendas;
* preparação das tabelas auxiliares;
* organização das tabelas para relacionamento no modelo;
* criação de uma estrutura que permite atualização com novos arquivos.

---

## Modelo de dados

Após o tratamento, as tabelas foram carregadas no Power BI e relacionadas no modelo.

A estrutura foi pensada para separar a tabela principal de vendas das tabelas auxiliares.

De forma geral, a lógica do modelo foi:

```text
Tabela de Vendas
↓
Clientes
Produtos
Vendedores
Metas
Calendário
```

A tabela de leads foi usada principalmente na página de conversão, junto com as informações do funil.

---

## Atualização do dashboard

O ponto principal do tratamento foi permitir atualização com novos arquivos.

Para atualizar a base de vendas, basta adicionar um novo arquivo na pasta `data/vendas`, mantendo o mesmo padrão dos arquivos anteriores.

Depois disso, ao atualizar o Power BI, o Power Query deve:

```text
1. encontrar o novo arquivo;
2. aplicar os mesmos tratamentos;
3. incluir os dados na tabela consolidada;
4. atualizar os visuais do dashboard.
```

---

## Cuidados necessários

Para o processo funcionar corretamente, é importante manter:

* o mesmo nome e ordem das colunas nos arquivos de vendas;
* o mesmo tipo de dado esperado em cada coluna;
* a estrutura da pasta `data/`;
* os nomes das pastas `apoio` e `vendas`;
* os arquivos auxiliares no local correto.

Se os arquivos forem movidos ou renomeados, pode ser necessário ajustar a origem dos dados no Power Query.

---

## Observação

Todos os dados usados neste projeto são fictícios.

O tratamento foi montado para simular um cenário comum em empresas: arquivos de vendas sendo adicionados periodicamente a uma pasta e um dashboard sendo atualizado a partir dessa base.
