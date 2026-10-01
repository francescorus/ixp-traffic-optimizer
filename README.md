# Ottimizzazione Del Traffico Di Rete In Un IXP

[![Research](https://img.shields.io/badge/Research-Paper%20in%20Preparation-orange.svg)]()
[![Status](https://img.shields.io/badge/Project-Active%20Research-blue.svg)]()
[![Scope](https://img.shields.io/badge/Domain-IXP%20%7C%20Traffic%20Engineering-darkgreen.svg)]()

> **Progetto accademico e paper**  
> Università degli Studi di Padova – Dipartimento di Ingegneria dell'Informazione (DEI)  
> **Autore:** Francesco Russo  
> **Supervisione accademica:** Prof. Nicola Zingirian  
> **In collaborazione con:** MIX (Milan Internet Exchange)

---

## 📢 Novità in arrivo: Articolo Scientifico in preparazione

Questo repository è il punto di raccordo per l'attività di ricerca scaturita dal lavoro di tesi di laurea in Ingegneria Informatica condotto in stretta sinergia con il **MIX (Milan Internet Exchange)**.

* 📝 **Stesura del paper al via:** Visti i risultati e la bontà dell'approccio riscontrati sui dati di rete, **abbiamo avviato i lavori per la redazione di un articolo scientifico** che formalizzerà l'intero impianto metodologico e i test sperimentali.
* 🔒 **Dettagli metodologici e codice riservati:** Per tutelare l'originalità del contributo scientifico e garantire i requisiti di novità previsti dai circuiti di revisione accademica, i modelli matematici formali, le architetture algoritmiche, i dataset di validazione e il codice sorgente completo **verranno resi pubblici su questa pagina al completamento del processo editoriale**.

---

## 📌 Di cosa si tratta

Gli **Internet Exchange Point (IXP)** sono nodi nevralgici dell'infrastruttura globale di telecomunicazioni: connettono fisicamente su scala metropolitana centinaia di Internet Service Provider (ISP), Content Delivery Network (CDN) e operatori cloud per consentire lo scambio diretto e bilaterale di massicci volumi di traffico.

All'aumentare esponenziale dei flussi multimediali e dei requisiti di latenza, la gestione del carico sulle dorsali interne di interconnessione di un IXP presenta sfide critiche:
* **Asimmetria dei flussi:** La concentrazione dei volumi verso specifici nodi può generare saturazioni localizzate improvvise.
* **Topologie complesse ad alta affidabilità:** La presenza di apparati ridondati e percorsi alternativi rende non banale la ripartizione bilanciata del carico senza degradare le prestazioni.
* **Limiti dell'instradamento convenzionale:** Le policy tradizionali basate unicamente sul cammino minimo o su metriche statiche spesso faticano a prevenire la formazione di colli di bottiglia prima che questi abbiano impatto sul servizio.

---

## 🎯 Il nostro approccio

Il progetto affronta il problema dell'**ingegneria del traffico all'interno della Peering LAN del MIX** proponendo un framework integrato che combina:

1. **Modellazione matematica avanzata:** Una formulazione rigorosa dell'instradamento che quantifica il costo della congestione di rete e determina un'allocazione bilanciata dei flussi, massimizzando il margine di sicurezza rispetto alle capacità fisiche dei collegamenti.
2. **Framework applicativo dedicato:** Una piattaforma software completa progettata per consentire agli operatori di rete di importare la topologia, simulare diversi scenari di carico "what-if" e calcolare in modo deterministico le configurazioni ottimali.
3. **Analisi e validazione empirica:** Lo studio del comportamento del sistema su configurazioni e vincoli operativi reali dell'infrastruttura del MIX.

---

## 📬 Contatti

Per informazioni:

* **Francesco Russo** – Università degli Studi di Padova  
* **Prof. Nicola Zingirian** – Dipartimento di Ingegneria dell'Informazione (DEI)
