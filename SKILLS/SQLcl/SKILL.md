---
name: sqlcl
description: >
  Práca s Oracle databázou cez SQLcl MCP. Pokrýva všetky operácie cez SQLcl MCP:
  vytváranie a správu spojení, spúšťanie SQL dotazov, prácu so schémami a ďalšie.
  Použi tento skill vždy keď používateľ pracuje s Oracle SQLcl MCP — či už ide o
  spojenia, dotazy, schémy alebo iné databázové operácie.
  Triggery: "vytvor spojenie", "pripoj sa", "spusti SQL", "zobraz tabuľky", "schéma",
  "Oracle databáza", "SQLcl", "SQL MCP", "create connection", "run query".
---

# SQLcl MCP Skill

Tento skill popisuje ako vytvoriť a uložiť pomenované databázové spojenie v Oracle SQLcl cez MCP.

## Vytvorenie nového spojenia

**Keď používateľ chce vytvoriť nové spojenie, VŽDY najprv zobraz interaktívny formulár pomocou `visualize:show_widget`.** Formulár obsahuje polia: Názov spojenia, Server, Port (default 1521), Service name / SID (prepínač), Používateľ, Heslo. Formulár priebežne generuje príkaz a po odoslaní ho automaticky spustí cez `sendPrompt`.

Správny príkaz na vytvorenie a uloženie spojenia je `conn` s flagmi `-save` a `-savepwd`:

```sql
conn -save <NAZOV_SPOJENIA> -savepwd <USER>/<HESLO>@<HOST>:<PORT>/<SERVICE_NAME>
```

### Príklad

```sql
conn -save TEST -savepwd TEST/SIRAB@192.168.0.8:1521/ORC1
```

Tento príkaz:
- Pripojí sa na databázu
- Uloží spojenie pod zadaným názvom
- Uloží heslo (flag `-savepwd`)

Po vytvorení spojenia ho vždy otestuj príkazom:

```sql
CONNMGR TEST <NAZOV_SPOJENIA>
```

A oznám používateľovi výsledok — či je spojenie funkčné alebo nie.

### Úspešná odpoveď vyzerá takto:
```
Name: TEST
Connect String: 192.168.0.8:1521/ORC1
User: TEST
Password: ******
Connected.
```

## Výpis uložených spojení

```sql
CONNMGR LIST
```

## Pripojenie na uložené spojenie

```sql
conn -name TEST
```

alebo cez MCP `connect` tool s `connection_name: "TEST"`.

## Prehľad MCP toolov

Detailný popis toolov, ich rozdielov a dôležité poznámky sú v `references/tools.md`.
Prečítaj ho keď potrebuješ vedieť ktorý tool použiť, aký formát vracia, alebo ako pracovať s asynchrónnymi jobmi.
