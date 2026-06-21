# Análise de NPS de um E-commerce

Este projeto tem como objetivo identificar quais fatores da jornada de compra mais influenciam a satisfação dos clientes de um e-commerce, utilizando o NPS (Net Promoter Score) como principal indicador de experiência.

A análise busca entender quais sinais operacionais estão associados à insatisfação dos clientes, permitindo que a empresa atue de forma preventiva antes que problemas impactem a recompra, aumentem o volume de reclamações ou prejudiquem a percepção da marca.

Além de avaliar a relação entre NPS e indicadores como atraso na entrega, atendimento, reclamações e recompra, o projeto também busca gerar insights que apoiem áreas como Logística, Atendimento, Operações, Marketing e Estratégia na tomada de decisão orientada por dados.

Por fim, a análise explora como a satisfação do cliente pode impactar resultados de negócio, incluindo retenção, fidelização, recomendação da marca e potencial de crescimento no mercado.

A entrega principal está organizada nos notebooks, contemplando entendimento do negócio, definição da variável alvo, qualidade dos dados, análise exploratória e reflexão sobre uma possível solução preditiva.

## Descrição da base de dados

A base utilizada está em:

- `data/raw/desafio_nps_fase_1.csv`

Ela contém **2.500 registros** e **19 colunas**, com informações sobre clientes, pedidos, entrega, atendimento, recompra e satisfação.

Principais grupos de variáveis:

- **Cliente:** `customer_id`, `customer_age`, `customer_region`, `customer_tenure_months`
- **Pedido:** `order_id`, `order_value`, `items_quantity`, `discount_value`, `payment_installments`
- **Entrega:** `delivery_time_days`, `delivery_delay_days`, `freight_value`, `delivery_attempts`
- **Atendimento:** `customer_service_contacts`, `resolution_time_days`, `complaints_count`
- **Satisfação e recompra:** `nps_score`, `repeat_purchase_30d`, `csat_internal_score`

A variável central da análise é:

- `nps_score`: nota de satisfação do cliente, em escala de 0 a 10.

Para a análise, o NPS foi classificado em três grupos:

- **Detrator:** `nps_score <= 5`
- **Neutro:** `nps_score > 5 e < 8`
- **Promotor:** `nps_score >= 8`

## Metodologia utilizada

O projeto foi organizado em duas etapas principais.

### 1. Data Quality

Notebook:

- `notebooks/dataquality.ipynb`

Nesta etapa foi documentado o contexto da base e foram realizadas checagens iniciais, incluindo:

- quantidade de linhas e colunas;
- tipos de dados;
- valores ausentes;
- duplicidades;
- validação da escala do NPS;
- verificação de valores financeiros negativos;
- análise descritiva das variáveis numéricas;
- criação de variáveis derivadas para análise.

A base tratada é salva em:

- `data/processed/desafio_nps_fase_1_clean.csv`

### 2. Análise Exploratória dos Dados (EDA)

Notebook:

- `notebooks/eda_nps.ipynb`

Neste notebook estão concentradas os principais insights identificados na análise exploratória:

- distribuição geral do NPS;
- proporção de detratores, neutros e promotores;
- correlação entre variáveis operacionais e `nps_score`;
- comparação entre grupos de NPS;
- impacto de atraso na entrega;
- impacto de reclamações e contatos com atendimento;
- análise por região;
- relação entre NPS e recompra em 30 dias.

Os principais achados indicam que a satisfação do cliente está mais associada à experiência operacional do que ao perfil do cliente. Atrasos na entrega, reclamações, múltiplos contatos com atendimento e maior tempo de resolução aparecem como fatores importantes para a geração de detratores.

## Estrutura do projeto

```text
NPS Analysis/
├── data/
│   ├── raw/
│   │   └── desafio_nps_fase_1.csv
│   └── processed/
│       └── desafio_nps_fase_1_clean.csv
├── notebooks/
│   ├── dataquality.ipynb
│   └── eda_nps.ipynb
├── reports/
│   └── apresentacao/
├── README.md
└── requirements.txt
```

## Como reproduzir os resultados

1. Clone ou baixe este repositório.

2. Acesse a pasta do projeto:

```bash
cd "NPS Analysis"
```

3. Crie e ative um ambiente virtual, se desejar:

```bash
python -m venv .venv
```

No Windows:

```bash
.venv\Scripts\activate
```

4. Instale as dependências:

```bash
pip install -r requirements.txt
```

5. Execute os notebooks nesta ordem:

```bash
jupyter notebook notebooks/dataquality.ipynb
```

Depois:

```bash
jupyter notebook notebooks/eda_nps.ipynb
```

Também é possível abrir os notebooks diretamente pelo VS Code e executar as células em sequência.

O vídeo de apresentação deste projeto está salvo em `reports/apresentacao/`.

## Observação sobre modelo preditivo

O desafio também propõe uma reflexão sobre como prever o NPS antes da aplicação da pesquisa. Essa proposta está descrita no notebook `notebooks/eda_nps.ipynb`.

Foram consideradas duas abordagens:

- **Regressão:** estimar a nota contínua de `nps_score`, de 0 a 10.
- **Classificação:** categorizar clientes em grupos de satisfação ou identificar clientes com risco de se tornarem detratores.

Do ponto de vista de negócio, a classificação binária foi indicada como estratégia inicial por gerar uma resposta mais simples e acionável para áreas como logística, atendimento e CRM.
