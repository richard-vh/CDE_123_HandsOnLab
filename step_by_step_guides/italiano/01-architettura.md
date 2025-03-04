Sure! Here's the translation of the text into Italian:

---

# Architettura CDE

## Obiettivo

In questa sezione imparerai l'architettura flessibile di CDE e i suoi principali componenti.

## Indice

* [Introduzione al servizio CDE](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#introduzione-al-servizio-cde)
  * [Ambiente CDP](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#ambiente-cdp)
  * [Servizio CDP](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#servizio-cdp)
  * [Cluster Virtuale](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#cluster-virtuale)
  * [Lavori CDE](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#lavori)
  * [Risorse CDE](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#risorsa)
  * [Esecuzione dei Lavori](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#esecuzione-del-lavoro)
  * [Sessioni CDE](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#sessione-cde)
  * [Apache Iceberg](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#apache-iceberg)
  * [Interfaccia Utente CDE](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#interfaccia-utente-cde)
* [Sintesi](https://github.com/pdefusco/CDE119_ACE_WORKSHOP/blob/main/step_by_step_guides/italian/part01_cde_architecture.md#sintesi)

## Introduzione al Servizio CDE

Cloudera Data Engineering (CDE) è un servizio per Cloudera Data Platform che ti consente di inviare lavori batch a cluster virtuali auto-scaling. CDE ti consente di dedicare più tempo alle tue applicazioni e meno tempo all'infrastruttura.

Cloudera Data Engineering ti consente di creare, gestire e pianificare lavori Apache Spark senza l'onere di creare e mantenere cluster Spark. Con Cloudera Data Engineering, definisci cluster virtuali con una gamma di risorse CPU e memoria, e il cluster si ridimensiona automaticamente in base alle necessità per eseguire i carichi di lavoro Spark, aiutandoti a controllare i costi cloud.

Il Servizio CDE è accessibile dalla Home Page di CDP cliccando sull'icona blu "Data Engineering".

![alt text](../../img/cdp_lp_0.png)

La Landing Page di CDE ti consente di accedere, creare e gestire Cluster Virtuali CDE. All'interno di ciascun Cluster Virtuale CDE, puoi creare, monitorare e risolvere i problemi relativi a Lavori Spark e Airflow.

Il Cluster Virtuale è collegato all'Ambiente CDP. Ogni Cluster Virtuale CDE è mappato a un massimo di un Ambiente CDP, mentre un Ambiente CDP può essere mappato a uno o più Cluster Virtuali.

Questi sono i componenti principali nel Servizio CDE:

##### Ambiente CDP
Un sottoinsieme logico del tuo account del provider cloud, che include una rete virtuale specifica. Gli ambienti CDP possono trovarsi su AWS, Azure, RedHat OCP e Cloudera ECS. Per maggiori informazioni, consulta [Ambienti CDP](https://docs.cloudera.com/management-console/cloud/overview/topics/mc-core-concepts.html). In pratica, un ambiente è equivalente a un Data Lake, poiché ogni ambiente è automaticamente associato ai propri servizi SDX per la Sicurezza, la Governance e la Lineage.

##### Servizio CDE
Il cluster Kubernetes a lunga durata e i servizi che gestiscono i cluster virtuali. Il servizio CDE deve essere abilitato su un ambiente prima di poter creare qualsiasi cluster virtuale.

##### Cluster Virtuale
Un cluster individuale auto-scaling con intervalli predefiniti di CPU e memoria. I Cluster Virtuali in CDE possono essere creati e eliminati su richiesta. I lavori sono associati ai cluster. Fino alla versione 1.18 di CDE, era disponibile solo un tipo di Cluster Virtuale. Dalla versione 1.19, puoi scegliere tra due Livelli di Cluster:

*Core (Livello 1)*: Le opzioni di trasformazione e ingegneria basate su batch includono:
* Cluster Auto-scaling
* Spot Instances
* SDX/Lakehouse
* Ciclo di vita dei Lavori
* Monitoraggio
* Orchestrazione dei flussi di lavoro

*Tutti gli Scopi (Livello 2)*: Sviluppo tramite sessioni interattive e distribuzione di carichi di lavoro sia batch che in streaming. Questa opzione include tutte le opzioni del Livello 1 con l'aggiunta di:
* Sessioni Shell - CLI e Web
* JDBC/SparkSQL (in arrivo a ottobre 2023 con CDE 1.20)
* IDE (in arrivo a ottobre 2023 con CDE 1.20)

I cluster Core sono consigliati come ambienti di produzione. I cluster All Purpose sono invece progettati per essere utilizzati come ambienti di sviluppo e test.
Per maggiori informazioni sulle versioni CDE 1.19.1 e 1.19.2, visita questa pagina nella [documentazione](https://docs.cloudera.com/data-engineering/cloud/release-notes/topics/cde-whats-new-1.19.html).

##### Lavori
Codice applicativo insieme a configurazioni e risorse definite. I lavori possono essere eseguiti su richiesta o pianificati. L'esecuzione di un singolo lavoro viene chiamata esecuzione del lavoro.

##### Risorsa
Una raccolta definita di file, come un file Python o un'applicazione JAR, dipendenze e qualsiasi altro file di riferimento necessario per un lavoro.

##### Esecuzione del Lavoro
Un'esecuzione singola di un lavoro.

##### Sessione CDE

Le sessioni interattive CDE offrono agli ingegneri dei dati punti finali flessibili per iniziare a sviluppare applicazioni Spark da qualsiasi luogo: in un terminale web-based, CLI locale, IDE preferito e anche tramite JDBC da strumenti di terze parti.

##### Apache Iceberg

Apache Iceberg è un formato di tabella cloud-native e ad alte prestazioni per organizzare dataset analitici su scala petabyte su un file system o un object store. Combinato con Cloudera Data Platform (CDP), gli utenti possono costruire un'architettura di open data lakehouse per analisi multi-funzionali e per distribuire pipeline end-to-end su larga scala.

L'Open Data Lakehouse su CDP semplifica l'analisi avanzata su tutti i dati con una piattaforma unificata per dati strutturati e non strutturati e servizi dati integrati per abilitare qualsiasi caso d'uso di analisi, da ML, BI ad analisi in streaming e in tempo reale. Apache Iceberg è il segreto dell'open lakehouse.

Iceberg è compatibile con una varietà di motori di calcolo, tra cui Spark. CDE ti consente di distribuire Cluster Virtuali abilitati Iceberg.

Per maggiori informazioni, visita la [documentazione](https://iceberg.apache.org/).

##### Interfaccia Utente CDE

Ora che hai compreso le basi di CDE, dedica qualche momento a familiarizzare con la Landing Page di CDE.

La Home Page offre una panoramica a livello alto di tutti i Servizi e Cluster CDE. È stata ridisegnata nella versione 1.19 per includere anche scorciatoie per azioni diverse, come la creazione di Lavori e Risorse CDE o la visita alla documentazione.

In alto, hai scorciatoie per creare Lavori e Risorse CDE.

![alt text](../../img/new_home_119.png)

Scorri verso il basso fino alla sezione Cluster Virtuali CDE e nota che tutti i Cluster Virtuali e ciascun Ambiente CDP / Servizio CDE associato sono mostrati.

![alt text](../../img/new_home_119_2.png)

Successivamente, apri la pagina di Amministrazione sulla scheda a sinistra. Questa pagina mostra anche i Servizi CDE a sinistra e i Cluster Virtuali associati a destra.

![alt text](../../img/service_cde.png)

Apri la pagina Dettagli Servizio CDE e nota le seguenti informazioni e collegamenti chiave:

* Versione CDE
* Intervallo di Autoscaling dei nodi
* Data Lake e Ambiente CDP
* Grafici di Graphana. Clicca su questo link per ottenere un dashboard delle risorse Kubernetes del Servizio in esecuzione.
* Scheduler delle Risorse. Clicca su questo link per visualizzare l'interfaccia Web di Yunikorn.

![alt text](../../img/service_cde_2.png)

Scorri verso il basso e apri la scheda Configurazioni. Nota che qui vengono definiti i Tipi di Istanza e gli intervalli di Autoscaling delle Istanze.

![alt text](../../img/cde_configs.png)

Per saperne di più su altre configurazioni importanti del servizio visita [Abilitare un Servizio CDE](https://docs.cloudera.com/data-engineering/cloud/enable-data-engineering/topics/cde-enable-data-engineering.html) nella Documentazione CDE.

Torna alla pagina di Amministrazione e apri la pagina Dettagli Cluster di un Cluster Virtuale.

![alt text](../../img/cde_virtual_cluster_details.png)

Questa vista include altre informazioni importanti sulla gestione del cluster. Da qui puoi:

* Scaricare i binari CLI di CDE. Il CLI è consigliato per inviare lavori e interagire con CDE. È trattato nella Parte 3 di questa guida.
* Visita la documentazione API per imparare a conoscere l'API CDE e costruire richieste di esempio sulla pagina Swagger.
* Accedi all'interfaccia utente di Airflow per monitorare i tuoi Lavori Airflow, configurare connessioni personalizzate, variabili e altro ancora.  

Apri la scheda Configurazione. Nota che puoi scegliere tra Cluster di tipo Core e All Purpose.
Inoltre, questa vista fornisce opzioni per impostare gli intervalli di autoscaling di CPU e memoria, la versione di Spark e le opzioni Iceberg.
CDE supporta Spark 2.4.8, 3.2.3, 3.3.0 e 3.5.1.

![alt text](../../img/vc_details_1.png)

![alt text](../../img/vc_details_2.png)

![alt text](../../img/vc_details_3.png)

Per saperne di più sull'Architettura CDE visita [Creazione e Gestione di Cluster Virtuali](https://docs.cloudera.com/data-engineering/cloud/manage-clusters/topics/cde-create-cluster.html) e [Raccomandazioni per la Scalabilità dei Deployment CDE](https://docs.cloudera.com/data-engineering/cloud/deployment-
