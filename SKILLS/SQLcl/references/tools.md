# SQLcl MCP — prehľad toolov a ich rozdiely

## Zoznam toolov

| Tool | Popis |
|---|---|
| `list-connections` | Zoznam uložených spojení |
| `connect` | Pripojenie na uložené spojenie podľa názvu |
| `run-sql` | Spustenie SQL dotazu, vracia výsledky ako CSV |
| `run-sqlcl` | Spustenie SQLcl CLI príkazov (`conn`, `CONNMGR`, `host`, atď.) |
| `run-sql-async` | Asynchrónne spustenie SQL na pozadí, vracia `job_id` |
| `schema-information` | Info o aktuálne pripojenej schéme |
| `disconnect` | Odpojenie od databázy |

## run-sql vs run-sqlcl vs run-sql-async

- **`run-sql`** — iba SQL príkazy (SELECT, INSERT, UPDATE...), výsledok okamžite vo formáte CSV (hlavičky v úvodzovkách, hodnoty oddelené čiarkami)
- **`run-sqlcl`** — SQLcl CLI príkazy aj SQL; použiť keď treba `conn`, `CONNMGR`, `host` a podobné
- **`run-sql-async`** — SQL spustený na pozadí, vráti `job_id`; výsledok zistíš cez `JOBS`:

```sql
jobs                  -- zoznam všetkých jobov
jobs -id <id>         -- stav konkrétneho jobu
jobs logs -id <id>    -- výsledok/logy jobu
jobs cancel -id <id>  -- zrušenie bežiaceho jobu
```

## Dôležité poznámky

- Príkaz `conn -save` vyžaduje aktívny SQLcl proces (cez MCP `run-sqlcl` tool)
- Port je štandardne `1521` pre Oracle
- `SERVICE_NAME` a `SID` sú rozdielne — pre service name použi `/`, napr. `@host:1521/ORC1`
- Pre SID použi `:`, napr. `@host:1521:ORC1`
- Názov spojenia je case-sensitive
- `CONNMGR IMPORT` slúži len na import z JSON súborov exportovaných zo SQL Developer — nie na priame vytvorenie spojenia
