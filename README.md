# Network Traffic Optimization in IXP Peering LANs

[![Research](https://img.shields.io/badge/Research-Paper%20Coming%20Soon-brightgreen.svg)]()
[![Status](https://img.shields.io/badge/Status-Under%20Peer%20Review-orange.svg)]()
[![Framework](https://img.shields.io/badge/Stack-Node.js%20%7C%20React%20%7C%20PostgreSQL-blue.svg)]()
[![Optimization](https://img.shields.io/badge/Optimization-MIQP%20%2F%20SCIP-red.svg)]()

> **Progetto accademico e di ricerca**  
> Università degli Studi di Padova – Dipartimento di Ingegneria dell'Informazione (DEI)  
> **Autore:** Francesco Russo  
> **Supervisione:** Prof. Nicola Zingirian  
> **In collaborazione con:** MIX (Milan Internet Exchange)

---

## 📢 Novità in arrivo: Articolo Scientifico (Stay Tuned!)

Questo repository documenta l'attività di ricerca originata dal lavoro di tesi di laurea in Ingegneria Informatica e condotta in collaborazione con il **MIX (Milan Internet Exchange)**.

A valle dei risultati ottenuti nella mitigazione della congestione tramite programmazione non lineare mista a interi (**MIQP**):

* 🚀 **Un articolo scientifico formale è attualmente in fase di finalizzazione/sottomissione.**
* 🔒 **Disponibilità del codice completo:** Per preservare l'originalità della ricerca (*prior art*, policy editoriali sui double-blind review) e la riservatezza delle matrici di rete industriali, la codebase completa, i dataset di validazione e le istruzioni dettagliate di riproduzione verranno resi accessibili pubblicamente in questo repository in coincidenza con la pubblicazione del paper.
* 📬 **Richieste di accesso anticipato:** Ricercatori o referenti del settore interessati a consultare la documentazione metodologica possono contattare gli autori per concordare l'accesso.

---

## 📌 Panoramica del Progetto

Gli **Internet Exchange Point (IXP)** costituiscono nodi nevralgici dell'ecosistema di Internet, consentendo l'interconnessione diretta a livello 2 tra Internet Service Provider (ISP), reti CDN e Cloud Provider.

Questo lavoro introduce una soluzione completa per la **modellazione e l'ottimizzazione del carico di traffico** all'interno dell'infrastruttura di commutazione di un primario IXP europeo:
1. **Modello MIQP Convesso:** Definizione di una funzione di costo quadratica sul coefficiente di saturazione dei link di uplink, calibrata per prevenire la formazione di colli di bottiglia e penalizzare severamente i rami sovraccarichi.
2. **Instradamento deterministico su topologie ad albero:** Sfruttamento delle proprietà delle architetture basate su **MLAG** per garantire assenza di loop di switching e consentire la determinazione dinamica dei coefficienti di routing $P_{j,w}^{x,d}$ tramite visita in ampiezza (BFS).
3. **Piattaforma di Gestione Reattiva:** Progettazione di un'architettura web modulare (React + Node.js REST stateless + PostgreSQL) integrata con il solutore esatto **SCIP** (Branch-and-Cut e rilassamento continuo con Simplesso).

---

## 🏗️ Schema Architetturale Sintetico

```text
┌──────────────────────┐         REST / JSON         ┌────────────────────────┐
│   Frontend Web       │ ◄─────────────────────────► │    Backend Engine      │
│  (React / Topologia) │                             │   (Node.js Stateless)  │
└──────────────────────┘                             └───────────┬────────────┘
                                                                 │
                                ┌────────────────────────────────┴───────────────────────────────┐
                                ▼                                                                ▼
                     ┌──────────────────────┐                                         ┌─────────────────────┐
                     │  Database Relazionale│                                         │   Solutore SCIP     │
                     │  (PostgreSQL - 3NF)  │                                         │   (Ottimizzatore)   │
                     └──────────────────────┘                                         └─────────────────────┘
