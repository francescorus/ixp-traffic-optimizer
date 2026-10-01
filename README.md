# Network Traffic Optimization in IXP Peering LANs

[![Node.js](https://img.shields.io/badge/Node.js-v18+-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18+-blue.svg)](https://react.dev/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14+-336791.svg)](https://www.postgresql.org/)
[![SCIP](https://img.shields.io/badge/Solver-SCIP%20OptSuite-orange.svg)](https://scipopt.org/)
[![Status: Work in Progress](https://img.shields.io/badge/Research-Paper%20in%20Progress-informational.svg)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **Progetto accademico e di ricerca**  
> Università degli Studi di Padova – Dipartimento di Ingegneria dell'Informazione (DEI)  
> **Autore:** Francesco Russo  
> **Supervisione accademica:** Prof. Nicola Zingirian  
> **In collaborazione con:** MIX (Milan Internet Exchange)

---

## 🔬 Origine del Progetto & Sviluppi Futuri (Research in Progress)

Questo repository raccoglie il lavoro nato inizialmente come **tesi di laurea triennale in Ingegneria Informatica** presso l'Università degli Studi di Padova, sviluppata in collaborazione con il **MIX (Milan Internet Exchange)**.

A seguito dei riscontri positivi e della solidità dei risultati ottenuti nella formalizzazione matematica e nell'allocazione del carico di rete, **la ricerca è attualmente attiva e in fase di estensione**:
* 📄 **Accademic Paper (Work in Progress):** Il modello matematico, la strategia di linearizzazione e i risultati sperimentali sono attualmente oggetto di formalizzazione per la stesura di un articolo scientifico destinato alla pubblicazione.
* 🚀 **Evoluzione del Framework:** L'attività prosegue con test su scenari di traffico scalabili, affinamento dei tempi di convergenza di SCIP e integrazione di metriche avanzate di traffic engineering per architetture IXP di nuova generazione.

---

## 📌 Panoramica del Progetto

Gli **Internet Exchange Point (IXP)** rappresentano snodi cardine dell'infrastruttura globale di Internet, consentendo a Internet Service Provider (ISP), Content Delivery Network (CDN) e carrier di scambiare traffico direttamente tramite *peering*.

Questo progetto propone un framework integrato per la **modellazione, visualizzazione e ottimizzazione del bilanciamento di traffico** all'interno della Peering LAN del MIX. Attraverso la formalizzazione di un problema di ottimizzazione matematica non lineare mista a variabili intere (**MIQP - Mixed-Integer Quadratic Programming**), il sistema determina l'allocazione ottimale dei flussi di traffico sui link di interconnessione, prevenendo colli di bottiglia e minimizzando la congestione complessiva della rete.

---

## 🧠 Modello Matematico & Risoluzione

### 1. Funzione Obiettivo Quadratica Convessa
La saturazione dei link di uplink viene penalizzata mediante una funzione quadratica del rapporto di utilizzo:

$$\min \sum_{x, d} \left( \frac{B_{x,d}}{L_{x,d}} \right)^2$$

* **Perché quadratica convessa:** A differenza di un approccio lineare, la crescita quadratica penalizza progressivamente e con severità i rami che si avvicinano alla saturazione, favorendo una ripartizione uniforme del carico. Inoltre, la convessità garantisce che ogni minimo locale coincida con l'ottimo globale.

### 2. Instradamento e Coefficienti di Routing
Sfruttando la topologia logica ad albero priva di cicli (garantita a livello 2 dall'adozione di architetture con switch ridondati in **MLAG**), il cammino tra ciascuna coppia di nodi $(j, w)$ è univoco. I coefficienti binari di instradamento:

$$P_{j,w}^{x,d} \in \{0, 1\}$$

vengono calcolati dinamicamente dal backend tramite visita in ampiezza (**Breadth-First Search, BFS**) sul grafo gerarchico, evitando la preallocazione di matrici dense statiche in memoria.

### 3. Solutore SCIP
Il problema MIQP è risolto in modo esatto tramite **SCIP (Solving Constraint Integer Programs)** impiegando tecniche di **Branch-and-Cut**, presolving e rilassamento continuo risolto con l'**algoritmo del Simplesso**.

---

## 🏗️️ Architettura del Sistema

L'applicazione è strutturata come una piattaforma web modulare e reattiva:

```text
┌─────────────────┐       HTTP / REST       ┌───────────────────────┐
│                 │  ───────────────────►   │                       │
│  React Frontend │                         │     Node.js Backend   │
│   (vis-network) │  ◄───────────────────   │   (Express, child_pr) │
└─────────────────┘      JSON Payload       └───────────┬───────────┘
                                                        │
                              ┌─────────────────────────┴────────────────────────┐
                              ▼                                                  ▼
                   ┌──────────────────────┐                           ┌─────────────────────┐
                   │  PostgreSQL Storage  │                           │   SCIP Optimization │
                   │ (Relational Topology)│                           │       Engine        │
                   └──────────────────────┘                           └─────────────────────┘
