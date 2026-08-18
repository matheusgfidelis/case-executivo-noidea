# Trilha 2 — Logística e SLA

**Tech Challenge Fase 1 | Case E-commerce Olist**
Responsável: Vinicius

Cobre só a trilha 2 (atraso na entrega x avaliação do cliente). Crescimento e
Receita, Pagamentos e Satisfação são de outras pessoas do grupo.

---

## Conteúdo

```
trilha2_logistica_sla/
├── README.md
├── analise_atraso_review.ipynb   <- notebook já executado
└── figuras/                      <- 2 gráficos em PNG e SVG
```

O notebook **já vem executado** — abre e vê tudo. Para rodar de novo, coloque
estes 2 CSVs do Kaggle na mesma pasta:

- `olist_orders_dataset.csv`
- `olist_order_reviews_dataset.csv`

Dependências: `pandas`, `seaborn`, `matplotlib`, `scipy`.

Para os slides, use os arquivos **`.svg`** (não perdem nitidez ao ampliar).

---

## Resultado

Base: 95.824 pedidos entregues com avaliação (2016–2018).

| Indicador | Valor |
|---|---|
| Taxa de atraso | 6,66% |
| Nota média geral | 4,16 |
| **Nota média — no prazo** | **4,29** |
| **Nota média — atrasado** | **2,27** |

**Correlação**

| Métrica | Coeficiente |
|---|---|
| Spearman (atraso em dias × nota) | −0,176 |
| Ponto-bisserial (atrasou sim/não × nota) | −0,392 |

Ambas com p < 0,001. A nota é ordinal (1 a 5), por isso Spearman e não Pearson.

**Nota média por faixa de atraso**

| Faixa | Nota média |
|---|---|
| Adiantado 4+ dias | 4,30 |
| Adiantado 1-3 dias | 4,13 |
| No prazo (dia exato) | 4,04 |
| Atraso 1-3 dias | 3,29 |
| Atraso 4-7 dias | 2,10 |
| Atraso 8+ dias | 1,70 |

---

## Os 3 pontos para a apresentação

1. **O atraso é o que mais destrói a satisfação.** Nota cai de 4,29 para 2,27 —
   dois pontos inteiros em uma escala de 5.
2. **54% dos pedidos atrasados recebem nota 1**, contra 7% dos entregues no prazo.
3. **O que importa é furar o prazo, não por quantos dias.** A nota cai de uma vez
   no primeiro dia de atraso e depois quase não piora.

**Recomendação:** a meta deve ser reduzir a *quantidade* de pedidos atrasados, não
o número médio de dias de atraso. Todo o ganho está em não cruzar o prazo.

📊 `figuras/01_nota_por_faixa_atraso` — gráfico principal
📊 `figuras/02_distribuicao_notas` — o contraste 54% x 7%

---

## Onde investir para ter retorno financeiro

> Os números desta seção vêm de uma análise complementar (decomposição do lead
> time por etapa, recorte por UF e exposição de receita) que **não está no
> notebook** — ele foi mantido enxuto no escopo da correlação. Se precisar
> reproduzir ou defender estes valores, me chame.

### 1. Malha de transporte — e não SLA de vendedor

Tempo médio de cada etapa, em dias:

| Etapa | No prazo | Atrasado | Diferença | % do tempo extra |
|---|---|---|---|---|
| Aprovação (pagamento) | 0,42 | 0,51 | +0,09 | 0,4% |
| Manuseio (vendedor → transportadora) | 2,60 | 5,53 | +2,93 | 12,8% |
| **Transporte (até o cliente)** | **7,98** | **27,78** | **+19,80** | **86,8%** |

Quando um pedido atrasa, o trecho transportadora → cliente leva **27,8 dias em
vez de 8**. Isso concentra **87% de todo o tempo extra**.

**Conclusão de investimento:** apertar o vendedor endereça 13% do problema. O
dinheiro tem que ir para malha logística e gestão de transportadora.

### 2. Rio de Janeiro — o alvo concreto

| | RJ | SP |
|---|---|---|
| Pedidos | 12.211 | 40.266 |
| Taxa de atraso | **11,9%** | 4,4% |
| Lead time médio | **15,2 dias** | 8,8 dias |
| Nota média | 3,97 | 4,25 |
| Receita | **R$ 2,03 milhões** | R$ 5,74 milhões |

Alagoas tem a pior taxa do país (20,8%), mas são apenas 394 pedidos — corrigir
lá tem impacto marginal. O **Rio** opera com **1,8x a taxa de atraso nacional**
sobre **R$ 2 milhões de receita**, e demora **74% mais que São Paulo** para
entregar.

São Paulo, ao lado, prova que 4,4% é alcançável. É problema de operação, não de
geografia — e por isso é resolvível com investimento.

### 3. A meta certa: reduzir a quantidade de atrasos, não os dias

| Faixa | Pedidos | Nota média |
|---|---|---|
| Atraso 4-7 dias | 1.748 | 2,10 |
| Atraso 8-15 dias | 1.601 | **1,67** |
| Atraso 16+ dias | 1.180 | **1,73** |

O dano **satura em ~2 semanas**: atrasar 16+ dias tem nota praticamente igual a
atrasar 8-15 dias. Quando o cliente já desistiu, atrasar mais não piora.

**Conclusão de investimento:** iniciativa de "acelerar pedidos já atrasados" não
traz retorno. Todo o ganho está em **não cruzar o prazo**.

### Exposição financeira

| Item | Valor | % da receita |
|---|---|---|
| Receita da base analisada | R$ 15.289.974 | 100% |
| Receita em pedidos atrasados | R$ 1.113.868 | 7,3% |
| **Receita em pedidos com nota ≤ 2** | **R$ 2.302.630** | **15,1%** |

### ⚠️ Como NÃO apresentar isso

**Não apresente nenhum destes números como ROI.** Dois motivos:

1. **A receita do pedido atrasado não foi perdida** — a venda aconteceu. O que
   existe é risco sobre receita futura, não prejuízo realizado.
2. **Não temos dado de custo logístico**, então é impossível calcular retorno
   sobre investimento.

Além disso, testei se o cliente insatisfeito compra menos depois: a diferença na
taxa de recompra deu **p = 0,25 — não significativa**. Não é possível provar o
efeito de churn com estes dados.

**O argumento honesto é exposição e risco, não ROI:**

> "R$ 2 milhões de receita no Rio operando com o dobro da taxa de atraso
> nacional, quando o estado vizinho prova que dá para fazer três vezes melhor.
> 87% desse atraso está no transporte."

Isso sustenta uma conversa de investimento. Um número de ROI inventado desmonta
na primeira pergunta da banca.

---

## Duas decisões que valem explicar

**1. Só pedidos entregues.** Filtramos `order_status == 'delivered'` com data de
entrega preenchida (96.470 de 99.441). Não faz sentido medir atraso de entrega em
pedido que não foi entregue.

**2. Atraso comparando datas, não horas.** O prazo prometido
(`order_estimated_delivery_date`) vem sempre com hora `00:00`. Se comparássemos os
timestamps direto, quase toda entrega feita *no* dia prometido apareceria como
atrasada e a taxa de atraso ficaria inflada. Por isso normalizamos as duas datas
antes de subtrair.

⚠️ Se outra trilha calcular atraso de outra forma, os números não vão fechar
entre as partes do trabalho. Vale alinhar antes de juntar tudo.

---

## Limitações

- Dados de 2016–2018: descrevem o período, não o mercado atual.
- Correlação não é causalidade. Atraso e nota baixa podem ter causas em comum
  (categoria do produto, distância, vendedor).
