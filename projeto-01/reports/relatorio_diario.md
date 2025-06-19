# Relatório Diário - Projeto de Análise de Dados – O Mercado

## Atividades Realizadas – Data: 2025-06-10
- Acessei a plataforma oficial do projeto e revisei o escopo da primeira etapa.
- Baixei e organizei as três planilhas fornecidas: `clientes`, `transacoes` e `resumo_compras`.
- Criei uma estrutura de pastas no Google Drive para armazenar os arquivos e manter a organização dos dados.
- Configurei um repositório no GitHub para versionamento e documentação do projeto.
- Iniciei a etapa de **conexão e importação de dados** entre planilhas no Google Sheets, conforme solicitado no escopo.
- Utilizei a função `IMPORTRANGE` combinada com `QUERY` para trazer os dados de forma dinâmica e automatizada:

  ```
  =QUERY(IMPORTRANGE("URL_DA_PLANILHA"; "NOME_DA_ABA!INTERVALO"); "SELECT *"; 1)
  ```
---

## Atividades Realizadas - Data: 2025-06-11
- Realizei uma análise inicial das tabelas do projeto com foco na detecção de valores nulos. Para isso, utilizei as fórmulas `COUNTA()` e `COUNTBLANK()` para verificar a presença de células preenchidas e vazias, respectivamente.

- Na tabela `clientes`, identifiquei uma inconsistência na coluna `salario_anual_dolar`:
  - A fórmula `=COUNTA(E2:E2241)` indicava menos valores do que o total esperado.
  - Para confirmar, utilizei `=COUNTBLANK(E2:E2241)` e detectei **24 células vazias**.
  - Posteriormente, filtrei essas linhas para visualização dos registros incompletos, mas ainda não realizei alterações nos dados.

- Na tabela `transacoes`, repeti a análise para identificar inconsistências:
  - A fórmula `=COUNTA(B2:B22128)` indicava menos valores do que o total esperado.
  - Para confirmar, utilizei `=COUNTBLANK(B2:B22128)` e detectei **7 células vazias**.
  - Como a tabela original é importada via `IMPORTRANGE` (que não permite edição direta), criei uma nova aba filtrada para poder manipular os dados sem alterar a fonte original:

  ```excel
  =FILTER(
    transacoes_original!A1:D;
    (transacoes_original!A1:A <> "") *
    (transacoes_original!B1:B <> "") *
    (transacoes_original!C1:C <> "") *
    (transacoes_original!D1:D <> "")
  )
  ```

- Na tabela `resumo_compras`, não foram encontradas células vazias.

## Atividades Realizadas - Data: 2025-06-12
- Iniciei a verificação de registros duplicados utilizando:

  ```excel
  =ARRAYFORMULA(IF(A2:A22128=""; ""; IF(COUNTIF(A2:A22128; A2:A22128) > 1; "Duplicado"; "Único")))
  ```

- **Explicação da abordagem**:
  - A fórmula analisa cada valor na coluna A e verifica se ocorre mais de uma vez. Se sim, marca como `"Duplicado"`; caso contrário, `"Único"`. Ignora células vazias.

- Para validar, criei um gráfico de rosca que indicou **0,9% de duplicatas**.
- Filtrei as 9 duplicações identificadas e criei uma nova aba tratada:

  ```excel
  =FILTER(
    resumo_compras_original!A1:G;
    (ROW(resumo_compras_original!A1:A) < 2242) + (ROW(resumo_compras_original!A1:A) > 2250)
  )
  ```

---

## Atividades Realizadas - Data: 2025-06-13
- Padronizei os formatos das colunas na nova aba tratada:
  - Formato numérico para colunas com valores.
  - Formato de data para colunas de data.

---

## Atividades Realizadas - Data: 2025-06-14
- Identifiquei o `id_cliente` como chave primária para integrar as tabelas `clientes_tratados`, `resumo_compras_tratados` e `transacoes_tratados`.
- Automatizei a união de tabelas usando `ARRAYFORMULA` + `PROCV`:

  ```excel
  =ARRAYFORMULA(SE(A2:A=""; ""; PROCV(A2:A; resumo_compras_tratados!A:B; 2; FALSO)))
  ```

- Ajustei os intervalos de cada aba de acordo com a localização do `id_cliente` em cada planilha.
- Corrigi erros de fórmula e validei os dados integrados para evitar falhas.

---

## Atividades Realizadas - Data: 2025-06-16
- Criei novas variáveis derivadas para enriquecer a análise do comportamento dos clientes.

### Variáveis Criadas:

- **mes_transacao**: mês da transação a partir da data.

  ```excel
  =TEXTO(data_transacao; "MM")
  ```

- **ano_transacao**: ano da transação.

  ```excel
  =ANO(data_transacao)
  ```

- **ultima_transacao**: data da última compra por cliente.

  ```excel
  =MAXIFS(data_transacao; id_cliente; id_cliente)
  ```

- **frequencia**: número total de compras por cliente.

  ```excel
  =CONT.SE(intervalo_id_cliente; id_cliente)
  ```

- **gasto_total_estimado**: soma dos gastos por categoria.

  ```excel
  =ARRAYFORMULA(total_vinho + total_frutas + total_carnes + total_peixes + total_doces + total_outros)
  ```

---