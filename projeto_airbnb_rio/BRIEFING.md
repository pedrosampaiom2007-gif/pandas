# Demanda DADOS-042: Diagnóstico de preços do Airbnb no Rio de Janeiro

> **Empresa fictícia**, criada para simular uma demanda real de trabalho.

| Campo | Valor |
| --- | --- |
| **Solicitante** | Diretoria de Expansão, Maré Hospedagens (empresa fictícia de gestão de imóveis para temporada) |
| **Responsável** | Analista de Dados (você) |
| **Prioridade** | Alta |
| **Prazo** | 2 sprints (2 semanas) |
| **Fonte dos dados** | [Inside Airbnb](https://insideairbnb.com/get-the-data/), Rio de Janeiro: `listings.csv.gz` e `calendar.csv.gz` (licença CC BY 4.0) |

---

## 1. Contexto

A Maré Hospedagens administra apartamentos de temporada para proprietários no Rio de Janeiro e quer **ampliar a carteira em 2026**. Hoje o preço das diárias é definido "no feeling" e a diretoria não sabe:

- em quais bairros vale mais a pena captar imóveis;
- quanto cobrar por tipo de imóvel;
- quanto o preço sobe em datas de alta demanda (Carnaval e Réveillon).

A empresa baixou os dados públicos do Airbnb, mas **eles chegam sujos**: preços em texto com `$` e vírgula, percentuais como texto, colunas `t`/`f`, listas guardadas como string, nulos e anúncios com preços absurdos. Antes de qualquer análise, **a base precisa ser tratada e documentada**.

## 2. Objetivo

Entregar uma **base tratada e confiável** dos anúncios do Rio e um **relatório com respostas às perguntas de negócio** abaixo, para apoiar a decisão de expansão.

## 3. Perguntas de negócio

| # | Pergunta | Quem vai usar |
| --- | --- | --- |
| P1 | Quais são os **10 bairros mais caros e os 10 mais baratos** (preço mediano por noite)? | Expansão |
| P2 | Como o preço varia por **tipo de quarto** (casa inteira, quarto privativo, compartilhado) **em cada bairro**? | Precificação |
| P3 | **Superhosts** cobram mais e têm avaliações melhores? | Operações |
| P4 | Quais são as **comodidades mais comuns** e quais estão ligadas a **preços maiores** (ex.: piscina, vista para o mar, ar-condicionado)? | Captação de imóveis |
| P5 | Quanto o preço e a ocupação mudam **por mês**, principalmente no **Carnaval e no Réveillon**? | Precificação |
| P6 | Quanto custa a diária mediana em **dólar**, para campanhas voltadas a estrangeiros? | Marketing |

## 4. Regras de tratamento (qualidade de dados)

A base tratada **só é aceita** se cumprir todas as regras:

| # | Regra | Colunas |
| --- | --- | --- |
| R1 | Preço convertido de texto (`"$1,234.00"`) para `float` | `price` |
| R2 | Percentuais convertidos de texto (`"95%"`) para `float` entre 0 e 1 | `host_response_rate`, `host_acceptance_rate` |
| R3 | Colunas `t`/`f` convertidas para `0`/`1` com dicionário de mapeamento | `host_is_superhost`, `instant_bookable`, `host_identity_verified` |
| R4 | Datas convertidas para `datetime` | `host_since`, `first_review`, `last_review` |
| R5 | Sem linhas duplicadas e sem `id` repetido | `id` |
| R6 | Anúncios **sem preço** removidos (não é possível estimar) | `price` |
| R7 | Nulos nas notas de avaliação **tratados e justificados** (remover, preencher ou manter, com explicação) | `review_scores_*` |
| R8 | Outliers de preço identificados pelo **método IQR**, com decisão documentada (remover ou limitar) | `price` |
| R9 | Comodidades transformadas de string para lista (regex + `str.split`) | `amenities` |
| R10 | Número de banheiros extraído do texto (`"1.5 baths"` vira `1.5`) | `bathrooms_text` |
| R11 | Coluna nova `anos_como_anfitriao`, calculada a partir de `host_since` | nova |
| R12 | **Log de tratamento**: quantas linhas existiam antes e depois de cada etapa | todas |

## 5. Entregáveis

1. **Notebook** `notebooks/airbnb_rio_tratamento_e_analise.ipynb`, organizado em seções, com cada decisão explicada em markdown.
2. **Base tratada** em `dados/tratados/listings_tratado.csv`.
3. **Base em SQLite** em `dados/tratados/airbnb_rio.db` (tabela `listings`), com **3 consultas SQL** de exemplo no notebook.
4. **Log de tratamento**: tabela com etapa, linhas antes, linhas depois e linhas removidas.
5. **Dicionário de dados** das colunas finais (nome, tipo, descrição), preenchido no `README.md`.
6. **Relatório executivo** no `README.md`: resposta curta para P1 a P6, com números e 3 a 5 gráficos salvos em `relatorio/graficos/`.

## 6. Critérios de aceite

- [ ] O notebook roda do início ao fim sem erro (*Runtime > Run all* no Colab).
- [ ] Todas as regras R1 a R12 foram aplicadas e são verificáveis com `info()` e `isna().sum()` no fim do tratamento.
- [ ] Cada pergunta P1 a P6 tem **resposta numérica** e **um gráfico ou tabela**.
- [ ] Toda remoção de dados tem justificativa e aparece no log.
- [ ] O relatório executivo dá para entender **sem abrir o notebook**.

## 7. Fora do escopo

- Modelos de machine learning (previsão de preço fica para uma próxima demanda).
- Dashboards interativos.
- Cidades além do Rio de Janeiro.
