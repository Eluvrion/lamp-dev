# LAMPDev Zuccante

Ambiente **LAMP** locale basato su Docker Compose, pensato per esercitazioni e sviluppo in aula.

## Scopo del progetto

Questo repository avvia uno stack minimo per studenti con:

- **Nginx**
- **PHP-FPM 8.4**
- **MariaDB**

## Prerequisiti

È necessario avere installato un runtime per container:

- (Preferibile) Podman Desktop con Podman-Compose
- Docker Desktop (o Docker CLI utilizzando WSL2)
- Un client esterno per la gestione DB, ad esempio:
  - HeidiSQL
  - DBeaver
  - altro DB manager compatibile MySQL/MariaDB

## Avvio rapido

Se si utilizza Docker:
```bash
docker compose up -d
```
Se si utilizza Podman:
```bash
podman compose up -d
```
**Per utilizzare compose su Podman, è richiesto un plugin dedicato**. Tipicamente è installato di default nel caso si utilizzasse Podman Desktop.

Dopo l'avvio, lo stack è disponibile sul web all'indirizzo: [http://localhost](http://localhost)

## Utilizzo

Tutto il codice HTML e PHP va posizionato sotto la cartella `www/` presente nella sezione root del compose.
La cartella è navigabile nativamente, perciò il codice si può organizzare in "siti" utlizzando la struttura: 
- `www/esercizio-1`
- `www/esercizio-2`
- `www/esercizio-n`

## Arresto

Per fermare i container mantenendo i dati:
```bash
docker compose down
```

Per fermare **e cancellare** i dati del database:
```bash
docker compose down -v
```

## Xdebug

La build PHP include Xdebug e altri moduli utili pre-compilati dal workflow.
PHP è fornito come artefatto di questa repo, per accelerare i tempi di deploy (sia su ARM64 che x86_64)

Xdebug è configurato nativamente per accettare connessioni da VSCode e PHPStorm:

- **Porta debugger:** `9003`
- **IDE key:** `VSCODE`
- **Host client:** `host.docker.internal`

## Connessione al database

MariaDB è esposto sulla porta TCP `3306` proprio per consentire la connessione da strumenti esterni (HeidiSQL, DBeaver, ecc.).

Parametri di default:

- **Host:** `127.0.0.1`
- **Porta:** `3306`
- **Utente:** `root`
- **Password:** *(vuota)*
- **Database iniziale:** `school`

## Licenza
Il codice contenuto in questa repository `Dockerfile`, `docker-compose.yml`, 
file di configurazione e workflow CI è rilasciato sotto licenza **MIT** 
(vedi file [`LICENSE`](LICENSE)).

Il software contenuto nelle immagini Docker utilizzate (PHP, MariaDB, Nginx, 
estensioni, ecc.) mantiene le rispettive licenze originali dei progetti upstream.
