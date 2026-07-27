# The RPG logic cycle, in fixed format

Chapter 120 ("Things to know about Free Format RPG") shows the RPG logic cycle as a diagram, and says every Fully Free Format program still has to set `*inlr = *on;` because of it. This file exists purely to make that diagram concrete: a real, classic fixed-format program that leans entirely on the cycle, a primary file, and control levels (`L1`/`L2`), instead of writing its own read loop. Fully Free Format RPG cannot do any of this, there are no I-specs, no O-specs, and no primary files any more, this is deliberately "the old way".

Fixed-format specs are entered in specific, fixed columns (H/F/I/C/O). The listings below use the conventional spacing found in real RPG III/RPG IV listings, if you ever key this in yourself, use F4 prompting in RDi or SEU rather than counting columns by hand, small column differences between releases exist and are not the point of this example.


## Sample data

The program reads one physical file, `SALES`, with three fields: `STORE`, `DEPARTMENT`, `REVENUE`. Ten sample rows:

| STORE     | DEPARTMENT  | REVENUE |
| --------- | ----------- | ------- |
| AMSTERDAM | BOOKS       |  500.00 |
| AMSTERDAM | ELECTRONICS | 3000.00 |
| AMSTERDAM | TOYS        | 1000.00 |
| AMSTERDAM | TOYS        | 1500.00 |
| BERLIN    | BOOKS       |  700.00 |
| BERLIN    | TOYS        | 1100.00 |
| BRUSSELS  | BOOKS       |  600.00 |
| BRUSSELS  | ELECTRONICS | 1200.00 |
| BRUSSELS  | ELECTRONICS | 2500.00 |
| BRUSSELS  | TOYS        |  800.00 |

This order is not accidental: a primary file is processed strictly in whatever order it delivers records, and a control-level break only makes sense when equal key values already sit next to each other. `SALES` is keyed on `STORE` + `DEPARTMENT` (a composite key), which is exactly why the rows above are grouped by store, and within a store, by department.

- `STORE` becomes control level **L1**, the major (outermost) break.
- `DEPARTMENT` becomes control level **L2**, the minor break, nested inside L1.


## The program

### H-spec

```
H DATFMT(*ISO)
```

### F-specs

```
FSALES     IP  E           K DISK
FQSYSPRT   O      132        PRINTER OFLIND(*INOF)
```

- `SALES`: **I**nput, **P**rimary, **E**xternally described, **K**eyed, on **DISK**. There can only be one primary file in a program, the cycle reads it automatically, no explicit `READ` is coded anywhere below.
- `QSYSPRT`: **O**utput, program-described (blank format column, so the 132-character record length is stated explicitly), a **PRINTER** file. `OFLIND` names the overflow indicator, turned on automatically once the page fills up.

### I-specs

`SALES` is externally described, so its fields are already known from its DDS, normally no I-specs would be needed at all for it. The one thing I-specs still have to do here is assign two of those fields to a control level, so the cycle knows which fields to compare from one record to the next:

```
ISALES        01
I                                                 STORE                  L1
I                                                 DEPARTMENT             L2
```

- `STORE` is marked `L1`, `DEPARTMENT` is marked `L2`. From here on, `L1`/`L2` are not just labels, they are indicators the cycle turns on by itself, exactly like `*INLR`, whenever the corresponding field's value changes from the previous record.

### C-specs

```
C     L2                   Z-ADD 0           DEPTTOT    7 2
C     L1                   Z-ADD 0           STORETOT   9 2
C                          ADD  REVENUE      DEPTTOT
C                          ADD  REVENUE      STORETOT
C                          ADD  REVENUE      GRANDTOT  11 2
```

This is the classic, and slightly subtle, part of control-break programming:

- The first two lines look like they run "at level L2" and "at level L1", but `L2`/`L1` here are coded as ordinary conditioning indicators, not in the control-level column, so these two lines actually run at **detail time**. They just happen to only run when `L2`/`L1` is already on. Since a control level indicator, once turned on, stays on all the way through the detail calculations of the record that follows the break, `DEPTTOT` and `STORETOT` are reset to zero exactly once: on the very first record of a new department, resp. a new store, right before that record's own revenue is added in.
- The three `ADD` lines are fully unconditioned, they run for every single record, adding the current `REVENUE` into all three accumulators. `GRANDTOT` is never reset, it keeps growing for the entire run.
- There is deliberately no C-spec conditioned by `L2`, `L1` or `LR` in the *control level column*: nothing needs to be calculated at total time here, the O-specs below do all the work, by testing those same indicators directly.

### O-specs

```
OQSYSPRT   H      1P
O                                          'Sales report'          20
OQSYSPRT   D
O                    STORE                              10
O                    DEPARTMENT                          30
O                    REVENUE        Y                    45
OQSYSPRT   T      L2
O                                          'Department total'      30
O                    DEPTTOT        Y                    45
OQSYSPRT   T      L1
O                                          'STORE TOTAL'           30
O                    STORETOT       Y                    45
OQSYSPRT   T      LR
O                                          'GRAND TOTAL'           30
O                    GRANDTOT       Y                    45
```

- The `H` line prints the report heading once, on page overflow (`1P`).
- The `D` (detail) line is unconditioned: one line per record read, exactly like the table above.
- The three `T` (total) lines are each conditioned by a control level indicator, `L2` fires once per department, `L1` once per store (right after that store's last department line), `LR` exactly once, after the very last record, for the grand total. The cycle decides on its own when each of these run, based purely on the indicators the control-level breaks turn on.


## Walking through the cycle

With the ten sample rows above, the cycle (open → read → detail → total, repeated automatically) produces, in order:

```
AMSTERDAM   BOOKS         500.00
AMSTERDAM   ELECTRONICS  3000.00
Department total          500.00        <- L2 break: BOOKS -> ELECTRONICS (prints the total for BOOKS, the group just ended)
AMSTERDAM   TOYS         1000.00
Department total         3000.00        <- L2 break: ELECTRONICS -> TOYS
AMSTERDAM   TOYS         1500.00
Department total         2500.00        <- L2 break: TOYS -> (next store) AND L1 break: AMSTERDAM -> BERLIN
STORE TOTAL              6000.00        <- L1 total, right after the last L2 total of that store
BERLIN      BOOKS         700.00
BERLIN      TOYS        1100.00
Department total          700.00        <- L2 break: BOOKS -> TOYS
Department total         1100.00        <- L2 break AND L1 break: BERLIN -> BRUSSELS
STORE TOTAL              1800.00
BRUSSELS    BOOKS         600.00
BRUSSELS    ELECTRONICS  1200.00
Department total          600.00        <- L2 break: BOOKS -> ELECTRONICS
BRUSSELS    ELECTRONICS  2500.00
BRUSSELS    TOYS          800.00
Department total         3700.00        <- L2 break: ELECTRONICS -> TOYS
Department total          800.00        <- LR: end of file, L2, L1 and LR all turn on together
STORE TOTAL              5100.00
GRAND TOTAL              12900.00
```

A few things worth noticing:

- When a level breaks, its total-time processing (calculations, then output) always happens for the group that is *ending*, using the values already accumulated, before a single calculation runs for the new group.
- When two levels break on the same record (moving from `AMSTERDAM`/`TOYS` to `BERLIN`/`BOOKS`, both `STORE` and `DEPARTMENT` change), the more nested level fires first: `L2` (department) before `L1` (store), matching how the report should actually read.
- `LR` behaves exactly like one more, even higher, control level: it turns on together with every other level that is still open when the file runs out of records, so the last department and the last store still get their proper subtotal, right before the grand total.
- None of this — the open, the reads, the comparison of `STORE`/`DEPARTMENT` between records, the decision on which total-time code to run — is written anywhere in the program. It is exactly the "backbone" chapter 120 refers to, entirely implicit, driven by `IP` on the `SALES` F-spec and the `L1`/`L2` entries on its I-specs.
