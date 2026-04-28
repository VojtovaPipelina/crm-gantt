# Changelog – CRM Gantt

## v3 – 2026-04-28

### WAIT-CRM task visual refinements
Follow-up polish on the WAIT-CRM blocker task added in v2.

| Field | Old value | New value |
|-------|-----------|-----------|
| `source` | `"WAIT"` | `"ANACRM"` |
| Activity cell style | plain | red background `#fdecea`, red left border (`--waiting-bar`), bold — same pattern as Critical rows |
| Bar color detection | `t.source === 'WAIT'` | `t.id === 'WAIT-CRM'` (source change required new detection) |

### Calendar columns extended
After the +5 week shift, tasks 50–53 land in October 2026 but the hardcoded `WEEKS` array ended at `2026-09-28`.

| Added weeks |
|-------------|
| `2026-10-05` |
| `2026-10-12` |

### Estimated End — dynamic calculation
`summary-end` card was hardcoded. Now computed in `updateSummary()` from the latest `x_weeks` date across all visible tasks (+6 days to show end of that week). Responds to role/layer/source filters automatically.

---

## v2 – 2026-04-28

### Schedule shift: ANACRM tasks +5 weeks
CRM team cannot deliver source data on time. Data available from week of **2026-06-01** (originally 2026-04-27).
All tasks depending on CRM data provisioning shifted **+5 weeks (+35 days)**.

**Tasks shifted (x_weeks dates +35 days):**

| Task | Description | Old start | New start |
|------|-------------|-----------|-----------|
| 8    | RAW: ADF pipeline CRM unity catalog → Dbx RAW | 2026-04-27 | 2026-06-01 |
| 10   | RAW: Dafne orchestration (ANACRM) | 2026-05-18 | 2026-06-22 |
| 12   | RAW: Validation of Dbx DEV data (ANACRM) | 2026-05-25 | 2026-06-29 |
| 14   | RAW: Import to Metacroc (ANACRM) | 2026-05-25 | 2026-06-29 |
| 16   | RAW: Metacroc descriptions (ANACRM) | 2026-05-25 | 2026-06-29 |
| 18   | RAW: Send data from TEST CRM to TEST GDP | 2026-06-01 | 2026-07-06 |
| 20   | RAW: DBx TEST data testing and validation (ANACRM) | 2026-06-01 | 2026-07-06 |
| 22   | RAW: PREPROD – PROD Release (ANACRM) | 2026-06-15 | 2026-07-20 |
| 23   | RAW: PREPROD – PROD Release (GRPDWH) | 2026-06-15 | 2026-07-20 |
| 24   | RAW: DBx PROD data validation (ANACRM) | 2026-06-15 | 2026-07-20 |
| 25   | RAW: DBx PROD data validation (GRPDWH) | 2026-06-15 | 2026-07-20 |
| 28   | BASE: Logical model impact analysis & redesign | 2026-06-01 | 2026-07-06 |
| 30   | BASE: Physical model changes and Metacroc mappings | 2026-06-15 | 2026-07-20 |
| 31   | BASE: Metacroc mappings RAW→BASE (GRPDWH) | 2026-06-29 | 2026-08-03 |
| 32   | BASE: Create/update data objects in Metacroc | 2026-06-15 | 2026-07-20 |
| 34   | BASE: Generate/update BASE DBX tables | 2026-06-15 | 2026-07-20 |
| 36   | BASE: Create Metacroc mappings (RAW→BASE, ANACRM) | 2026-06-29 | 2026-08-03 |
| 37   | BASE: Release Metacroc mapping scripts to DBX | 2026-07-06 | 2026-08-10 |
| 38   | BASE: Historized data from Synapse – init mapping | 2026-07-20 | 2026-08-24 |
| 39   | BASE: Historized data from Synapse – insert _h table | 2026-07-27 | 2026-08-31 |
| 40   | BASE: DEV data set validation (ANACRM) | 2026-08-03 | 2026-09-07 |
| 41   | BASE: DEV data set validation (GRPDWH) | 2026-08-10 | 2026-09-14 |
| 42   | BASE: Dafne orchestrations – DBX Jobs (ANACRM) | 2026-08-03 | 2026-09-07 |
| 43   | BASE: Dafne orchestrations – DBX Jobs (GRPDWH) | 2026-08-17 | 2026-09-21 |
| 45   | BASE: Definition of DQ checks + implementation | 2026-06-15 | 2026-07-20 |
| 46   | BASE: QG for BASE LDM of Customer related areas | 2026-06-22 | 2026-07-27 |
| 48a  | BASE: QG physical data model (ANA) | 2026-08-24 | 2026-09-28 |
| 48b  | BASE: QG physical data model (BE, ANACRM) | 2026-08-24 | 2026-09-28 |
| 49a  | BASE: QG physical data model (ANA, GRPDWH) | 2026-08-24 | 2026-09-28 |
| 49b  | BASE: QG physical data model (BE, GRPDWH) | 2026-08-24 | 2026-09-28 |
| 50   | BASE: PROD Release (ANACRM) | 2026-09-07 | 2026-10-12 |
| 51   | BASE: PROD Release (GRPDWH) | 2026-09-07 | 2026-10-12 |
| 52   | BASE: DBX PROD validation (ANACRM) | 2026-09-07 | 2026-10-12 |
| 53   | BASE: DBX PROD validation (GRPDWH) | 2026-09-07 | 2026-10-12 |

**Tasks NOT shifted (pure GRPDWH, independent of CRM data):**
`2a, 2b, 3a, 3b, 5, 7, 9, 11, 13, 15, 17, 19, 21`

> Note: Task 23 is GRPDWH source but depends on task 22 (ANACRM), therefore shifted.
> Tasks 24 and 25 both depend on task 23, therefore also shifted.

---

### New task: WAIT-CRM
Added external blocker task to make the reason for delay explicit.

| Field | Value |
|-------|-------|
| ID | `WAIT-CRM` |
| Activity | Waiting for CRM data provisioning |
| Weeks | 2026-04-27 → 2026-05-25 (5 weeks) |
| Color | Red (`#e53935`) |
| Depends on | QG-IA |

Task 8 deps updated: `QG-IA` → `QG-IA;WAIT-CRM`

---

## v1 – 2026-04-28

### Color changes

| Source | Element | Old color | New color |
|--------|---------|-----------|-----------|
| ANACRM | Gantt bar | `#4472C4` (blue) | `#f48fb1` (light pink) |
| ANACRM | Row background | `#dce6f3` | `#fce4ec` |
| GRPDWH | Gantt bar | `#70AD47` (green) | `#9c27b0` (purple) |
| GRPDWH | Row background | `#e2efda` | `#f3e5f5` |

Role column (ANA / BE) colors intentionally kept unchanged (blue `#4472C4` / green `#70AD47`).
