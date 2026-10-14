# P.R.O.T.E.G.E. — Plataforma de Rastreamento e Otimização Terapêutica em Geriatria na Atenção Primária

> **Engenharia de Dados como Infraestrutura Habilitadora para a Segurança do Paciente Geriátrico**  
> *Arquitetura Lakehouse Medallion em Databricks / Delta Lake aplicada a Dados Reais da PNAUM ($N = 8.747$)*

---

## 📌 Visão Geral do Projeto
O **P.R.O.T.E.G.E.** é uma solução de Engenharia de Dados e Inteligência Clinical Decision Support System (CDSS) desenvolvida para identificar, classificar e mitigar riscos associados ao uso de Medicamentos Potencialmente Inapropriados (MPIs) em idosos assistidos pela Atenção Primária à Saúde (APS).

O pipeline processa microdados populacionais da **Pesquisa Nacional sobre Acesso, Utilização e Promoção do Uso Racional de Medicamentos (PNAUM)**, aplicando os consensos internacionais de **Beers** e **STOPP/START** de forma automatizada e escalável.

---

## 🏗️ Arquitetura do Pipeline (Medallion Pattern)

```text
[ Microdados PNAUM ]
         │
         ▼
 ┌──────────────┐
 │ Camada BRONZE│  -> Ingestão Bruta, Higienização e Carga Incremental (Delta Lake)
 └──────┬───────┘
        │
        ▼
 ┌──────────────┐
 │ Camada SILVER│  -> Governança LGPD (SHA-256 + Salt) + CDSS (Beers & STOPP/START)
 └──────┬───────┘
        │
        ▼
 ┌──────────────┐
 │ Camada GOLD  │  -> Modelagem Dimensional (Star Schema: Fato e Dimensões SCD Tipo 2)
 └──────────────┘
