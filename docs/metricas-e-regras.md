# Métricas e Regras

Este documento resume as principais métricas e regras usadas no dashboard **Dashboard Performance Vendas**.

A ideia é deixar claro como os indicadores foram calculados, como os filtros funcionam e quais decisões foram tomadas na construção do relatório.

---

## Visão geral

O dashboard acompanha a performance comercial de uma empresa fictícia de hardware e produtos de escritório.

A análise foi dividida em três páginas principais:

* **Visão Geral de Vendas**
* **Desempenho de Vendedores**
* **Conversão de Leads**

O relatório foi construído para acompanhar vendas, faturamento, lucro, metas, desempenho de vendedores e conversão de leads.

---

## Faturamento Total

Representa o valor total vendido.

```text
Faturamento Total = Quantidade Vendida * Preço Unitário
```

Essa métrica é usada como principal indicador financeiro do dashboard.

---

## Total de Vendas

Representa a quantidade total de produtos vendidos.

```text
Total de Vendas = soma da coluna Quantidade
```

Neste projeto, essa métrica não representa a quantidade de pedidos, mas sim o volume total de itens vendidos.

---

## Custo Total

Representa o custo total dos produtos vendidos.

Essa métrica é usada como base para calcular o lucro.

---

## Lucro Total

Representa o resultado financeiro após descontar os custos.

```text
Lucro Total = Faturamento Total - Custo Total
```

---

## Margem de Lucro

Mostra quanto do faturamento ficou como lucro.

```text
Margem de Lucro = Lucro Total / Faturamento Total
```

Essa métrica ajuda a avaliar se o faturamento está crescendo com boa rentabilidade ou apenas com aumento de volume.

---

## Ticket Médio

Representa o faturamento médio por produto vendido.

```text
Ticket Médio = Faturamento Total / Total de Vendas
```

Como o Total de Vendas considera a quantidade de produtos vendidos, o ticket médio indica o valor médio por item vendido.

---

## Meta Atingida

A Meta Atingida compara o faturamento realizado com a meta prevista.

```text
Meta Atingida = Faturamento Total / Meta
```

A tabela de metas possui metas mensais para cada vendedor em todos os anos da base.

Essa métrica é usada para acompanhar o desempenho geral da operação e também o desempenho individual dos vendedores.

---

## Comparativo YoY

Os cards do dashboard mostram a variação em relação ao ano anterior.

```text
Variação YoY = (Valor do Ano Selecionado - Valor do Ano Anterior) / Valor do Ano Anterior
```

Quando não há um ano selecionado ou não existe ano anterior disponível para comparação, a variação fica em branco.

Nesses casos, o texto `vs. ano ant.` também é ocultado para evitar uma comparação sem referência.

---

## Taxa de Conversão

Mostra a proporção de leads que foram convertidos.

```text
Taxa de Conversão = Leads Convertidos / Total de Leads
```

---

## Taxa de Perda

Mostra a proporção de leads perdidos.

```text
Taxa de Perda = Leads Perdidos / Total de Leads
```

Essa métrica ajuda a acompanhar o quanto da base de leads não avançou até a conversão.

---

## Tempo Médio de Conversão

Representa o tempo médio entre a criação do lead e a data de conversão.

```text
Tempo Médio de Conversão = Data de Conversão - Data de Criação do Lead
```

No dashboard, o resultado é exibido em dias.

---

## Funil de Vendas

O funil mostra em qual etapa cada lead parou.

As etapas usadas foram:

```text
Contato Inicial
Qualificação
Apresentação
Proposta
Fechamento
```

A visualização ajuda a identificar em quais partes do processo comercial ocorre maior perda de leads.

---

## Motivos de Perda

O gráfico de motivos de perda mostra os principais motivos associados aos leads não convertidos.

Ele ajuda a entender se a perda está mais relacionada a preço, concorrência, falta de interesse ou outros fatores comerciais.

---

## Volume vs. Ticket

O gráfico **Volume vs. Ticket** compara os vendedores a partir de dois indicadores:

```text
Eixo X = quantidade de vendas
Eixo Y = ticket médio
```

As linhas pontilhadas representam as médias gerais.

Com isso, é possível observar diferentes perfis de vendedores, como:

* vendedores com alto volume e ticket menor;
* vendedores com baixo volume e ticket maior;
* vendedores acima da média nos dois indicadores;
* vendedores abaixo da média nos dois indicadores.

Essa visualização foi usada para comparar desempenho de forma mais completa do que apenas pelo faturamento.

---

## Ranking de Vendedores

O ranking de vendedores é ordenado pelo faturamento em ordem decrescente.

```text
Ranking = vendedores ordenados por Faturamento Total
```

Além do faturamento, a tabela também mostra indicadores como quantidade de vendas e percentual de meta atingida.

---

## Tooltip de Vendedor

A tabela de vendedores possui um tooltip personalizado.

Ao passar o mouse sobre um vendedor, o relatório exibe informações complementares, como:

* margem;
* ticket médio;
* tempo médio;
* percentual de vendas recorrentes;
* leads convertidos e perdidos.

A ideia foi manter a tabela principal mais limpa, deixando os detalhes adicionais no tooltip.

---

## Faturamento por Categoria

O gráfico de faturamento por categoria usa uma hierarquia com drill down.

A ordem da hierarquia é:

```text
Categoria → Subcategoria → Marca → Produto
```

Isso permite começar a análise em um nível mais geral e depois navegar até níveis mais detalhados, como marca ou produto.

---

## Eixos Dinâmicos

Alguns gráficos mudam o eixo de acordo com o filtro de ano.

A regra geral é:

```text
Com ano selecionado → mostrar meses
Sem ano selecionado → mostrar anos
```

Esse comportamento foi aplicado em gráficos como:

* faturamento;
* quantidade de vendas;
* faturamento vs. meta;
* volume de leads.

Os títulos desses gráficos também são dinâmicos, acompanhando o indicador e o período exibido.

---

## Alternância de Indicadores

Alguns visuais permitem trocar o indicador analisado.

Na página de Visão Geral, o gráfico principal permite alternar entre:

* faturamento;
* quantidade de vendas.

Na página de Leads, o gráfico por canal permite analisar:

* leads totais;
* leads convertidos;
* tempo médio de conversão.

Isso permite reaproveitar o mesmo espaço visual para responder perguntas diferentes.

---

## Tratamento dos Dados

A parte de tratamento foi feita no Power Query.

A regra principal foi montar um processo que permitisse atualizar o dashboard conforme novos arquivos fossem adicionados à pasta de dados.

O fluxo usado foi:

```text
1. Buscar todos os arquivos da pasta
2. Filtrar somente as planilhas de vendas
3. Transformar os arquivos
4. Combinar tudo em uma única tabela
5. Tratar e relacionar com as tabelas auxiliares
```

As tabelas auxiliares usadas no projeto incluem dados de clientes, vendedores, produtos, metas, leads, funil e imagens dos vendedores.

---

## Estrutura dos Dados

A pasta `data/` foi organizada em duas partes:

```text
data/
├── apoio/
└── vendas/
```

A pasta `vendas/` contém os arquivos anuais de vendas.

A pasta `apoio/` contém as tabelas auxiliares usadas no modelo, como clientes, produtos, vendedores, metas e leads.

---

## Observação sobre os dados

Todos os dados utilizados neste projeto são fictícios.

Isso inclui:

* nomes dos vendedores;
* fotos dos vendedores;
* dados de clientes;
* dados de vendas;
* dados de leads;
* metas;
* produtos.

As fotos e os nomes dos vendedores foram gerados com IA e usados apenas para fins visuais no dashboard.

---

## Objetivo das regras

As regras foram pensadas para manter o dashboard simples de usar e fácil de interpretar.

O objetivo não foi criar um modelo estatístico complexo, mas sim construir um relatório comercial completo, interativo e útil para acompanhar vendas, metas, vendedores e conversão de leads.
