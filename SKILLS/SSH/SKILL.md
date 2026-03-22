---
name: ssh
description: "Connect to a remote Linux server via SSH, optionally using a GNU screen session. Use this skill when the user says things like 'connect to server X', 'pripoj sa na server X', 'screen Y', 'run command on server X', 'spusti na serveri X'. Two modes: screen mode (long-running tasks, interactive work) and direct mode (simple commands)."
---

# SSH workflow (Desktop Commander, Windows)

## Výber módu

| Mód | Kedy použiť |
|-----|------------|
| **Screen mód** | Dlhé operácie (apt upgrade, DB export...), interaktívna spolupráca, príkazy kde používateľ sleduje výstup |
| **Priamy mód** | Jednoduché príkazy s rýchlym výstupom (status, config read, restart služby) |

---

## SCREEN MÓD

### Krok 1 — Otvor SSH spojenie

```
start_process(
    command="ssh -tt root@HOST",
    shell="powershell.exe",
    timeout_ms=10000
)
```
Ulož PID z výsledku (napr. PID=17136).

### Krok 2 — Nájdi alebo over screen session

Ak používateľ neurčil session, zisti dostupné:

```
interact_with_process(pid=PID, input="screen -ls", timeout_ms=5000)
```

Vyber session podľa názvu alebo nechaj používateľa vybrať.
Ak session je **Attached** alebo **Detached** — nevadí, použijeme `-X stuff`.


### Krok 3 — Posielaj príkazy do screen session

```
interact_with_process(
    pid=PID,
    input='screen -S SESSION_ID -X stuff "PRIKAZ; echo =DONE=\n"',
    timeout_ms=10000
)
```

`\n` na konci je povinné — simuluje Enter.
Marker `; echo =DONE=` je povinný pre všetky príkazy kde čítaš výstup (krok 4).

### Krok 4 — Čítaj výstup (polling do dokončenia)

Pre **krátke príkazy** (do ~5 sekúnd) stačí jedno volanie:

```
interact_with_process(
    pid=PID,
    input="screen -S SESSION_ID -X hardcopy /tmp/out.txt && cat /tmp/out.txt",
    timeout_ms=10000
)
```

Pre **dlhé príkazy** (apt upgrade, DB dump, kompilácia...) **polluj opakovane** kým sa neobjaví marker `=DONE=`:

```python
# Pseudokód — opakuj kým output neobsahuje =DONE=
while True:
    interact_with_process(
        pid=PID,
        input="screen -S SESSION_ID -X hardcopy /tmp/out.txt && cat /tmp/out.txt",
        timeout_ms=10000
    )
    if "=DONE=" in output:
        break
    wait 5-10 sekúnd, prípadne informuj používateľa o progrese
```

**Nikdy nepoužívaj pevný timeout ako záruku dokončenia** — príkaz môže trvať sekundy aj hodiny.

### Krok 5 — SSH zostáva otvorené

SSH spojenie **nezatváraj** po každom príkaze. Ostáva aktívne počas celej práce.
Zatvoriť iba na **explicitný pokyn používateľa** ("zatvori SSH", "exit", "skonči").

```
interact_with_process(pid=PID, input="exit", timeout_ms=5000)
```


---

## PRIAMY MÓD (bez screenu)

### Varianta A — Jednorázový príkaz (odporúčané pre jednoduché operácie)

```
start_process(
    command='ssh -T root@HOST "PRIKAZ"',
    shell="powershell.exe",
    timeout_ms=15000
)
```

Výstup je priamo v návratovej hodnote `start_process`. Nevyžaduje PID ani ďalšie volania.
Vhodné pre: `systemctl status X`, `cat /etc/config`, `df -h`, `uptime`, reštart služieb.

### Varianta B — Interaktívny shell bez screenu

Keď treba viac príkazov za sebou ale screen nie je k dispozícii:

```
# 1. Otvor SSH
start_process(
    command="ssh -tt root@HOST",
    shell="powershell.exe",
    timeout_ms=10000
)
# Ulož PID

# 2. Posielaj príkazy
interact_with_process(pid=PID, input="PRIKAZ\n", timeout_ms=10000)

# 3. Čítaj výstup
read_process_output(pid=PID, timeout_ms=5000)

# 4. Detekuj dokončenie dlhých príkazov — použi marker:
interact_with_process(pid=PID, input="PRIKAZ; echo =DONE=\n", timeout_ms=10000)
# Polluj read_process_output kým nevidíš =DONE= vo výstupe

# 5. Zatvori až na pokyn používateľa
interact_with_process(pid=PID, input="exit\n", timeout_ms=5000)
```

**Nevýhoda oproti screen módu:** používateľ nevidí výstup v reálnom čase na svojej obrazovke.


---

## Spoločné nastavenia

- Shell: vždy `powershell.exe`
- Autentifikácia SSH kľúčom — skontroluj `~/.ssh/config` používateľa na prítomnosť kľúča pre daný host
- `StrictHostKeyChecking no` v SSH configu — known_hosts konflikty sa ignorujú

## Prečo -X stuff a nie screen -x (attach)?

- `screen -x` zlyhá ak SSH samo beží v screene → "Attaching from inside of screen?"
- `screen -X stuff "prikaz\n"` pošle príkaz priamo bez attachovania — funguje vždy

## Parametre SSH

| Parameter | Použitie |
|-----------|----------|
| `ssh -tt root@HOST` | Interaktívny shell — vynúti pseudo-TTY |
| `ssh -T root@HOST prikaz` | Jednorázový príkaz, čistý výstup, bez TTY |

## Časté chyby

| Chyba | Príčina | Riešenie |
|-------|---------|----------|
| exit 255 | Host neexistuje / sieť nedostupná | Overiť IP/hostname |
| "Attaching from inside of screen?" | Nested screen attach | Použiť -X stuff |
| exit 127 (cmd shell) | Príkaz v úvodzovkách cez cmd.exe | Vždy použiť powershell.exe |
| Príkaz sa zdá dokončený ale nie je | Pevný timeout nestačil | Použiť polling + =DONE= marker |
| read_process_output vracia prázdno | Výstup bol konzumovaný skôr | Použiť screen + hardcopy namiesto priameho SSH |
