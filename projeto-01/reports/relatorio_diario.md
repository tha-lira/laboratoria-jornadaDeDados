# Relatório Diário - Projeto de Análise de Dados – O Mercado

# Relatório Diário - Projeto de Análise de Dados – O Mercado

## Atividades Realizadas - Data: 2025-06-10
- Fiz login na plataforma do projeto.
- Baixei e organizei as planilhas de dados.
- Iniciei a etapa de conexão e importação de dados conforme a meta, usando a função:
  - `IMPORTRANGE` para importar dados entre planilhas do Google Sheets.
- Organizei as pastas no Google Drive e configurei o repositório no GitHub para versionamento.

---

## Atividades Realizadas - Data: 2025-06-11
- Analisei as tabelas do projeto e identifiquei valores nulos utilizando:
  - `COUNTBLANK(intervalo)` para contar células vazias.
- Na tabela `clientes`, detectei **24 células vazias** na coluna **salario_anual_dolar**.
- Na tabela `transacoes`, detectei **7 células vazias** na coluna **id_cliente**.
- Registrei essas inconsistências para tratamento posterior.

---

## Atividades Realizadas - Data: 2025-06-12
- Tratei os valores nulos:
  - Substituí os 24 valores nulos de salário anual por 0, usando substituição direta na planilha.
  - Excluí as 7 linhas na tabela `transacoes` onde o `id_cliente` estava nulo.
- Iniciei a verificação de duplicados usando:
  - `COUNTIF(intervalo; valor)` para identificar valores repetidos.

---

## Atividades Realizadas - Data: 2025-06-13
- Removi 8 linhas duplicadas da tabela `resumo_compras`.
- Ajustei os formatos das colunas para:
  - Número: formato numérico padrão.
  - Data: formato de data padrão do Google Sheets.
- Garantindo a consistência dos dados para análises futuras.

---

## Atividades Realizadas - Data: 2025-06-14

- Identifiquei as colunas-chave para unir as tabelas, usando o `id_cliente` como chave nas abas `clientes`, `resumo_compras` e `transacoes`.
- Usei a função `ARRAYFORMULA` combinada com `PROCV` para automatizar a importação dos dados da aba `resumo_compras` para a aba `clientes`, trazendo as informações correspondentes com a fórmula:  

```
=ARRAYFORMULA(SE(A2:A=""; ""; PROCV(A2:A; resumo_compras!A:B; 2; FALSO)))
```

- Ajustei os intervalos e colunas para garantir que os dados fossem puxados corretamente considerando a posição dos IDs em cada aba.
- Corrigi erros de fórmula que surgiram no processo para assegurar que a união das tabelas fosse automática, eficiente e sem falhas.
- Finalizei a etapa garantindo que a aba `clientes` estivesse atualizada com as informações de `resumo_compras` e pronta para as próximas etapas do projeto.

---


## Atividades Realizadas - Data: 2025-06-16
- Iniciei a criação de novas variáveis derivadas a partir das tabelas existentes.
- As novas variáveis permitem observar padrões de comportamento dos clientes, facilitando a análise.

- As variáveis criadas foram:

  - mes_transacao: extraída a partir da data da transação com a função TEXTO(data_transacao; "MM"). Essa variável identifica o mês em que cada compra foi realizada.
  ```
	 =TEXTO(data_transacao; "MM")
  ```
  - ano_transacao: obtida com a função ANO(data_transacao), permitindo analisar a distribuição das compras ao longo dos anos.
  ```
	 =ANO(data_transacao)
  ```
  - ultima_transacao: representa a data da última compra de cada cliente. Calculada com a função MAXIFS(data_transacao; id_cliente; id_cliente), permite medir a recência de compra.
  ```
	 =MAXIFS(data_transacao; id_cliente; id_cliente)
  ```
  - frequencia: número total de compras por cliente, calculado com a função 
  ```
	 =CONT.SE(intervalo_id_cliente; id_cliente)
  ```
  - gasto_total_estimado: estimativa do valor total gasto por cliente, obtida pela soma das quantidades de produtos comprados em diferentes categorias (vinho, frutas, carnes, peixes, doces e outros), usando a função ARRAYFORMULA(total_vinho + total_frutas + total_carnes + total_peixes + total_doces + total_outros).
  ```
	 =ARRAYFORMULA(total_vinho + total_frutas + total_carnes + total_peixes + total_doces + total_outros)
  ```
---