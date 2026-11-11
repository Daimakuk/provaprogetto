# AI Academy - Esercitazione Git per il progetto finale

Simuliamo il lavoro del progetto: fork, clone, modifiche, commit, push, tag di consegna e miglioramenti su un ramo separato.

Non serve scrivere codice Python. Alla fine avrai tre commit personali, un tag `task1` e un ramo `extra-work`.

Le istruzioni sono in italiano; report e messaggi dei commit sono in inglese, come richiesto nel progetto.

## Prima di iniziare

- Servono un account GitHub, Git e un editor come VS Code.
- Esegui un comando alla volta. Se fallisce, fermati e chiedi al docente.
- Sostituisci i segnaposto con i tuoi dati.
- Salva i file nell'editor prima di usare Git.
- Questa è una repository di prova: domani partirai dal repository del progetto indicato dal docente.

## 1. Crea il tuo fork

Su GitHub:

1. Apri il repository condiviso dal docente.
2. Premi **Fork** e crea la copia nel tuo account.
3. Apri il tuo fork: nell'indirizzo deve comparire il tuo nome utente.
4. Premi **Code**, seleziona **HTTPS** e copia l'URL.

Il **fork** è la tua copia su GitHub; il **clone** sarà la copia sul PC.

## 2. Verifica Git e configura la tua identità

```bash
git --version
```

Deve comparire una versione. Configura nome ed email, sostituendo i valori:

```bash
git config --global user.name "Nome Cognome"
git config --global user.email "propria-email@example.com"
```

Puoi usare l'email associata al tuo account GitHub oppure quella privata noreply fornita da GitHub.

Controlla:

```bash
git config --global user.name
git config --global user.email
```

Questi dati identificano l'autore dei commit: **non effettuano il login a GitHub**.

## 3. Clona il tuo fork

Apri il terminale nella cartella dove vuoi conservare l'esercizio. Sostituisci `URL_DEL_TUO_FORK` con l'indirizzo HTTPS copiato:

```bash
git clone URL_DEL_TUO_FORK ai-academy-git-practice
cd ai-academy-git-practice
```

Il secondo argomento di clone stabilisce il nome della cartella locale. Se quella cartella esiste già, chiedi al docente: non cancellarla per ripetere la prova.

Controlla:

```bash
git remote -v
git branch --show-current
git status
```

**Risultato atteso:**

- `origin` punta al tuo fork, non al repository del docente.
- Il ramo principale normalmente si chiama `main`.
- La cartella è pulita: `working tree clean`.

Nei comandi seguenti usiamo `main`: se il tuo ramo principale ha un nome diverso, sostituiscilo.

Apri VS Code:

```bash
code .
```

Se il comando non viene riconosciuto, usa **File > Apri cartella** e seleziona la cartella clonata. Apri il terminale integrato. Tutti i prossimi comandi vanno eseguiti dentro questa cartella.

## 4. Inizia il Task 1: crea un report

```bash
mkdir reports
```

Se la cartella esiste già, usa quella presente.

In VS Code crea `reports/task1.md` con questo contenuto:

```markdown
# Task 1 report

Student: Nome Cognome

## Goal
Practice the Git workflow for the final project.

## Progress
I created my fork and cloned it onto my computer.
```

Sostituisci il nome, salva e controlla:

```bash
git status
```

Il report deve comparire tra i file non ancora tracciati: `untracked`.

## 5. Crea il primo commit e invialo

```bash
git add reports/task1.md
git diff --staged
git commit -m "docs: create task report"
```

- `add` prepara il file per il commit.
- `diff --staged` mostra cosa stai per salvare.
- `commit` registra una versione nella storia locale.

Se il terminale apre una vista scorrevole, premi `q` per uscire.

Verifica e invia:

```bash
git status
git log --oneline -3
git push
```

Se viene richiesta l'autenticazione, completa l'accesso a GitHub. Non inserire credenziali nei file del progetto.

**Controllo sul sito:** aggiorna il tuo fork e apri `reports/task1.md`. Deve contenere il testo appena scritto.

**Ricorda:** salvare nell'editor non equivale a fare commit; fare commit non equivale a fare push.

## 6. Modifica il report e crea il secondo commit

Aggiungi in fondo al file:

```markdown
## What I learned
A commit records a version locally.
A push sends commits to the remote repository.
A tag identifies a specific version.
```

Salva. Guarda la differenza rispetto all'ultimo commit:

```bash
git diff
```

Poi:

```bash
git add reports/task1.md
git diff --staged
git commit -m "docs: explain commit push and tag"
git log --oneline -3
```

Devi riconoscere i tuoi due commit più recenti.

## 7. Simula la scadenza: crea e invia il tag task1

Il secondo commit rappresenta la consegna alla fine del tempo assegnato.

```bash
git status
```

Deve risultare `working tree clean`. Se ci sono ancora modifiche da consegnare, salvale in un commit prima di creare il tag.

```bash
git tag -a task1 -m "Task 1 submission"
git push origin main
git push origin task1
```

Verifica:

```bash
git tag --list
git show --stat task1
```

**Controllo sul sito:** apri l'elenco dei tag nel tuo fork. Deve comparire `task1`.

### Regole da ricordare

- Il tag deve chiamarsi esattamente `task1`.
- Il messaggio del commit non deve necessariamente iniziare con `task1:`.
- Scrivere `task1` nel messaggio del commit **non crea il tag**.
- Il push del ramo mostrato sopra non invia automaticamente il tag annotato: lo inviamo con il comando dedicato.
- Il tag punta a un commit: non include modifiche non ancora committate.
- Non spostare o ricreare il tag per includere lavoro successivo.
- Se Git dice che `task1` esiste già, fermati e verifica con il docente. Non usare opzioni di forzatura.

## 8. Simula il lavoro aggiuntivo fuori aula

Crea un ramo separato:

```bash
git switch -c extra-work
git branch --show-current
```

Il secondo comando deve stampare `extra-work`.

Aggiungi al report:

```markdown
## Next steps
Practice branches and review the project requirements.
```

Salva, crea il terzo commit e invia il nuovo ramo:

```bash
git add reports/task1.md
git diff --staged
git commit -m "docs: add next steps"
git push -u origin extra-work
```

`-u` collega il ramo locale al corrispondente ramo remoto. Per i successivi invii da questo ramo potrai usare semplicemente `git push`.

**Controllo sul sito:** seleziona il ramo `extra-work`. Il report deve contenere la sezione `Next steps`.

Per questa esercitazione **non aprire pull request e non unire extra-work a main**.

## 9. Verifica che la consegna non sia cambiata

```bash
git log --oneline --graph --decorate --all -10
```

Devi riconoscere:

- il tag `task1` sul secondo commit personale;
- il ramo `extra-work` sul terzo commit personale.

Leggi il report della versione consegnata:

```bash
git show task1:reports/task1.md
```

**La sezione Next steps non deve comparire:** è stata aggiunta dopo.

Se sei nella vista scorrevole, premi `q` per uscire.

## 10. Passa da un ramo all'altro

Prima controlla di non avere modifiche da salvare:

```bash
git status
```

Torna al ramo principale:

```bash
git switch main
```

Nel report aperto nell'editor, `Next steps` non compare.

Torna al ramo aggiuntivo:

```bash
git switch extra-work
```

La sezione ricompare.

**Cambiare ramo cambia i file della cartella di lavoro. Non cancella il commit conservato nell'altro ramo.**

## 11. Consegna l'esercitazione

Invia al docente **il link del tuo fork su GitHub**, non il percorso della cartella sul PC.

- [ ] Il fork appartiene al mio account.
- [ ] Il report è presente e contiene il mio nome.
- [ ] Ho creato tre commit personali.
- [ ] Il tag `task1` è su GitHub e punta al secondo commit personale.
- [ ] Il ramo `extra-work` è su GitHub.
- [ ] Nel tag `task1` non compare `Next steps`.
- [ ] Nel ramo `extra-work` compare `Next steps`.
- [ ] So spiegare la differenza fra commit, push e tag.

## Domani, nel progetto finale

1. Fai commit frequenti, almeno ogni 30 minuti.
2. Aggiorna il report con risultati, problemi e limiti reali.
3. Alla scadenza salva lo stato raggiunto, anche se incompleto.
4. Crea e invia il tag del task: `task1`, `task2`, `task3` oppure `task4`.
5. Conserva il lavoro aggiuntivo fuori aula su un ramo separato, secondo le indicazioni del docente.
6. Non aggiungere chiavi API, password o l'ambiente `.venv` al repository.

### Esempio: chiusura del Task 2

**Questo è un riferimento per domani: non eseguirlo durante l'esercitazione.**

Eseguilo sul ramo concordato per il lavoro in aula. Prima di `git add .`, controlla che il `.gitignore` sia configurato e che non ci siano file sensibili o non necessari.

```bash
git status
git add .
git diff --staged
git commit -m "docs: record task 2 status at deadline"
git tag -a task2 -m "Task 2 submission"
git push origin HEAD
git push origin task2
```

Se non ci sono nuove modifiche, il commit non serve: crea il tag sul commit corrente.

`git push origin HEAD` invia il ramo attuale. Controlla su quale ramo stai lavorando prima della consegna. Un tag già presente non va sovrascritto.

## Tre comandi per mostrare il lavoro

```bash
git status
git log --oneline --graph --decorate --all -10
git show --stat task1
```

Rispondono a tre domande: che cosa è cambiato, come si è sviluppato il lavoro e quale versione è stata consegnata.
