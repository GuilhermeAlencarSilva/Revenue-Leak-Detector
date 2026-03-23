# 🚨 Revenue Leak Detector

## Financial Loss Intelligence Dashboard

> "Crescer receita é importante. Proteger margem é o que sustenta o negócio."

---

# 🎯 1. Contexto Executivo

Em muitas empresas, perdas financeiras não são explícitas. Elas se escondem em descontos mal calibrados, devoluções recorrentes, fretes ineficientes e decisões comerciais que priorizam volume em detrimento de margem.

Este projeto simula uma iniciativa de consultoria estratégica orientada a dados para responder à pergunta:

> **Onde a empresa está perdendo dinheiro sem perceber — e quanto isso custa?**

---

# 🧠 2. Hipótese de Negócio

A hipótese central é que uma parcela relevante da receita é corroída por ineficiências operacionais e comerciais — o chamado **Revenue Leakage**.

**Premissas:**

* Nem todo desconto é perda → existe desconto estratégico
* Nem todo frete é desperdício → depende da política logística
* Devoluções representam perda real de receita

---

# 🏗️ 3. Abordagem Analítica (DEASA)

**Definição:** Identificar e quantificar vazamentos financeiros

**Estruturação:**

* Receita
* Descontos
* Devoluções
* Frete
* Clientes

**Análise:**

* Métricas DAX padronizadas
* Modelagem estrela
* Normalização de dados (remoção de outliers)

**Soluções:**

* Score de vazamento financeiro
* Identificação de drivers de perda

**Apresentação:**

* Dashboard executivo em Power BI
* Storytelling orientado a decisão

---

# 🗂️ 4. Dataset (Simulação Realista)

Base sintética com ~100k registros simulando 12 meses de operação.

## Tabelas

### 🧾 Vendas (Fato)

* id_venda, data_venda
* id_cliente, id_produto, id_vendedor
* quantidade, preco_unitario
* desconto, receita, custo, lucro

### 👤 Clientes

* id_cliente, nome_cliente
* segmento, cidade, estado

### 📦 Produtos

* id_produto, nome_produto
* categoria, custo_unitario

### 🚚 Fretes

* id_venda, custo_frete

### 🔁 Devoluções

* id_devolucao, id_venda
* valor_devolucao

---

# 🧩 5. Modelagem de Dados

**Modelo Estrela (Star Schema)**

* Fato: Vendas
* Dimensões: Clientes, Produtos, Tempo, Vendedores
* Auxiliares: Fretes (1:1 com Vendas), Devoluções (1:N com Vendas)

**Boas práticas aplicadas:**

* Evitar many-to-many
* Chaves substitutas
* Tipagem correta (numérica vs texto)

---

# 📐 6. Métricas-Chave (DAX)

```DAX
Receita Total = SUM(vendas[receita])
Lucro Total = SUM(vendas[lucro])
Valor Desconto = SUM(vendas[desconto])
Custo Frete = SUM(fretes[custo_frete])
Custo Devoluções = SUM(devolucoes[valor_devolucao])
```

---

# ⚠️ 7. Revenue Leak Score (Modelo Proprietário)

Nem toda perda tem o mesmo impacto. Criamos um score ponderado:

```DAX
Revenue Leak Score =
VAR Desconto = [Valor Desconto] * 0.5
VAR Frete = [Custo Frete] * 0.3
VAR Devolucao = [Custo Devoluções]
RETURN Desconto + Frete + Devolucao
```

```DAX
Revenue Leak % = DIVIDE([Revenue Leak Score], [Receita Total])
```

**Interpretação:**

* < 10% → Saudável
* 10–20% → Atenção
* 20–30% → Alto
* > 30% → Crítico

---

# 📊 8. Dashboard Executivo

## Página 1 — Visão Geral

<img width="1032" height="772" alt="pag1" src="https://github.com/user-attachments/assets/f6165834-5b7c-4d55-9979-9f86e3d3bfd8" />

* KPIs: Receita, Lucro, Leak Score, Leak %
* Tendência mensal
* Breakdown por categoria

## Página 2 — Descontos

<img width="1036" height="769" alt="pag2" src="https://github.com/user-attachments/assets/89d7573c-c285-4cb1-9ed4-051559e2b433" />

* Ranking de vendedores
* Scatter: Receita vs Desconto
* Identificação de outliers

## Página 3 — Devoluções

<img width="802" height="769" alt="pag3" src="https://github.com/user-attachments/assets/f3a452d3-fe6a-4444-8a7e-770bca67f406" />

* Produtos com maior índice
* Taxa de devolução

## Página 4 — Estoque

<img width="804" height="769" alt="pag4" src="https://github.com/user-attachments/assets/44c8851c-844d-4c7f-be64-e0516c8d5c6a" />

* Produtos de baixo giro
* Capital parado

## Página 5 — Clientes

<img width="1021" height="769" alt="pag5" src="https://github.com/user-attachments/assets/92d41cc1-020c-4d9d-a07b-4bcac25873a9" />

* Receita vs Lucro
* Clientes não rentáveis

---

# 💡 9. Principais Insights Gerados

* Vendedores com política agressiva de desconto
* Produtos com alta devolução → possível problema de qualidade
* Clientes com alto volume e baixa margem
* Ineficiências logísticas impactando lucro

---

# 💰 10. Simulação de Impacto Financeiro

Exemplo de cenário:

> Redução de 20% nos descontos excessivos

Resultado estimado:

* Aumento direto no lucro
* Melhora no Revenue Leak %
* Ganho operacional relevante

---

# 🧠 11. Problemas de Dados Encontrados (e Correções)

* ❌ Fretes com valores irreais → normalizados
* ❌ Relações many-to-many → corrigidas
* ❌ Double counting no score → ajustado
* ❌ Tipos de dados incorretos → corrigidos

---

# 🚀 12. Diferenciais do Projeto

* Score analítico de vazamento financeiro
* Simulação de dados corporativos realistas
* Abordagem de consultoria estratégica
* Foco em decisão (não só visualização)

---

# 📢 13. Narrativa de Consultoria

Este projeto não é apenas um dashboard.

É uma simulação de como uma consultoria identificaria perdas financeiras ocultas e traduziria dados em decisões executivas.

---

# 🧑‍💻 14. Tecnologias

* Power BI
* Python (geração de dados)
* DAX

---

# 📌 15. Conclusão

Pequenas ineficiências operacionais podem gerar grandes impactos financeiros.

Empresas que medem apenas receita estão olhando para o topo do funil.

As que monitoram vazamentos financeiros controlam a lucratividade.

---

# 🔗 Contato

📬 Contato

Autor: Guilherme Alencar Cruz da Silva

LinkedIn:https://www.linkedin.com/in/guilherme-alencar-327413213/
---

⭐ Se este projeto te gerou insights, considere deixar uma estrela.
