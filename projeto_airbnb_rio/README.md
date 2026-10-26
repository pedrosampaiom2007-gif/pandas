# Quanto custa uma noite no Rio? Diagnóstico de preços do Airbnb

> 🚧 *Projeto em andamento. Preencha as seções marcadas com "preencher" ao concluir.*

Projeto prático de tratamento e análise de dados com **Python e pandas**, feito para fechar a trilha de Python para Data Science da Alura.
Simula uma demanda real de trabalho: a [Maré Hospedagens](BRIEFING.md) (empresa fictícia) quer saber **onde, quanto e quando cobrar** pelas diárias no Rio de Janeiro.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pedrosampaiom2007-gif/pandas/blob/main/projeto_airbnb_rio/notebooks/airbnb_rio_tratamento_e_analise.ipynb)

## 📌 A demanda

Os dados públicos do Airbnb chegam sujos (preços em texto, percentuais como string, `t`/`f`, listas guardadas como texto, nulos e preços absurdos). O trabalho foi:

1. **Tratar** a base seguindo 12 regras de qualidade ([veja o briefing](BRIEFING.md)).
2. **Responder** a 6 perguntas de negócio.
3. **Entregar** a base limpa em CSV e SQLite, com log de tratamento e dicionário de dados.

## 🛠️ Ferramentas

Python · pandas · NumPy · Matplotlib · Seaborn · Requests (API do Banco Central) · SQLAlchemy/SQLite · Google Colab

## 📊 Principais resultados

> *(preencher: 1 frase de impacto + número para cada pergunta)*

| Pergunta | Resultado |
| --- | --- |
| P1. Bairros mais caros e mais baratos | |
| P2. Preço por tipo de quarto e bairro | |
| P3. Superhost cobra mais? | |
| P4. Comodidades que valorizam o imóvel | |
| P5. Carnaval e Réveillon | |
| P6. Diária mediana em dólar | |

<!-- Exemplo de gráfico: ![Preço mediano por bairro](relatorio/graficos/p1_bairros.png) -->

## 🧹 Log de tratamento

> *(preencher com a saída de `pd.DataFrame(log_tratamento)`)*

| Etapa | Linhas antes | Linhas depois | Removidas |
| --- | --- | --- | --- |
| | | | |

## 📖 Dicionário de dados (base tratada)

> *(preencher com as colunas finais)*

| Coluna | Tipo | Descrição |
| --- | --- | --- |
| `id` | int | Identificador do anúncio |
| `price` | float | Preço da diária em R$ |
| | | |

## 📁 Estrutura

```
projeto_airbnb_rio/
├── BRIEFING.md              # a demanda: contexto, perguntas, regras e critérios de aceite
├── notebooks/
│   └── airbnb_rio_tratamento_e_analise.ipynb
├── dados/
│   ├── brutos/              # arquivos do Inside Airbnb (não versionados)
│   └── tratados/            # base limpa em CSV e SQLite
└── relatorio/
    └── graficos/            # gráficos usados neste README
```

## 📚 Fonte e licença dos dados

Dados de [Inside Airbnb](https://insideairbnb.com/), licença [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Extração usada: *(preencher a data)*.
