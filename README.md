# Case Executivo Olist

Este repositório reúne a análise exploratória e a apresentação de indicadores de negócio do e-commerce brasileiro usando o dataset público da Olist.

## Objetivo do projeto

O projeto busca responder perguntas estratégicas do negócio, como:

- Como a receita e o volume de pedidos evoluíram ao longo do tempo?
- Quais categorias e regiões geram mais faturamento?
- O atraso de entrega impacta negativamente a experiência do cliente?
- Quais métodos de pagamento e padrões de compra predominam?
- Como entender recorrência, recência e monetização dos clientes?

## Estrutura do projeto

```text
.
├── data/
│   ├── olist_customers_dataset.csv
│   ├── olist_geolocation_dataset.csv
│   ├── olist_order_items_dataset.csv
│   ├── olist_order_payments_dataset.csv
│   ├── olist_order_reviews_dataset.csv
│   ├── olist_orders_dataset.csv
│   ├── olist_products_dataset.csv
│   ├── olist_sellers_dataset.csv
│   └── ...
├── notebooks/
│   ├── 01_Crescimento_e_Receita_Evolucao_Mensal.ipynb
│   ├── 01_Crescimento_e_Receita_Ticket_Medio_por_Regiao.ipynb
│   ├── 02_Logistica_e_SLA_Atraso_vs_Review.ipynb
│   └── 03_Comportamento_e_Pagamentos_Metodos_e_Recompra.ipynb
├── Relatorio_Executivo.pptx
├── README.md
└── .git/
```

## Dados utilizados

Os dados provêm do dataset público da Olist, com tabelas como:

- pedidos
- itens de pedido
- clientes
- vendedores
- produtos
- pagamentos
- avaliações
- geolocalização

Essas bases permitem analisar desde crescimento e receita até logística, satisfação do cliente e comportamento de compra.

## Notebooks

### 1) Crescimento e receita

Arquivo: `notebooks/01_Crescimento_e_Receita_Evolucao_Mensal.ipynb`

Foca em:

- evolução mensal de pedidos
- receita acumulada e por mês
- ticket médio
- participação por categoria
- participação por região / UF
- principais produtos e vendedores

### 2) Ticket médio por região

Arquivo: `notebooks/01_Crescimento_e_Receita_Ticket_Medio_por_Regiao.ipynb`

Foca em:

- cálculo do ticket médio por região do Brasil
- consolidação por estado ou região
- comparação de faturamento e volume de pedidos

### 3) Logística e SLA

Arquivo: `notebooks/02_Logistica_e_SLA_Atraso_vs_Review.ipynb`

Foca em:

- atraso na entrega
- comparação entre pedidos no prazo e atrasados
- impacto do atraso na nota do cliente
- correlação entre atraso e avaliação

### 4) Comportamento, pagamentos e recompra

Arquivo: `notebooks/03_Comportamento_e_Pagamentos_Metodos_e_Recompra.ipynb`

Foca em:

- métodos de pagamento mais utilizados
- parcelamento
- análise de ticket por forma de pagamento
- RFM (recência, frequência e monetização)
- comportamento de recompra e relacionamento com o cliente

## Como executar

Recomenda-se usar o Jupyter Notebook ou Jupyter Lab a partir da raiz do projeto:

```bash
jupyter notebook
```

ou

```bash
jupyter lab
```

A partir daí, abra os notebooks dentro da pasta `notebooks/`.

## Dependências

As análises usam bibliotecas comuns de ciência de dados, como:

```bash
pip install pandas numpy matplotlib seaborn scipy openpyxl
```

Se preferir, também pode criar um ambiente virtual antes de instalar as dependências.

## Observações importantes

- Os notebooks foram desenvolvidos para rodar a partir da raiz do projeto.
- O caminho dos arquivos CSV assume que a pasta `data/` está no mesmo nível da pasta `notebooks/`.
- Alguns notebooks podem depender de arquivos auxiliares ou dados tratados específicos.

## Resultado esperado

O projeto entrega uma visão executiva do negócio da Olist, conectando:

- crescimento
- rentabilidade
- logística
- satisfação do cliente
- comportamento de pagamento e retenção

## Autor

Projeto desenvolvido no contexto de análise de dados e relatórios executivos para o case Olist.
