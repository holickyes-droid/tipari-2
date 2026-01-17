# SystemCore v4.1 — Data Audit & Inconsistency Report

## 1. Úvod
Tento audit mapuje nekonzistence napříč dokumentací a implementačními soubory SystemCore v4.1. Analyzované soubory: SystemCore_Project_Documentation_v4.1.md, SystemCore_Reviewer_Alignment_Report.md, SystemCore_Release_and_Maintenance_v4.1.md, SystemCore_Audit_and_Validation_v4.1.md, SystemCore_Governance_Framework_v4.1.md, SystemCore_Operational_Runbook_v4.1.md, SystemCore_DataModel_v4.1.md, SystemCore_UXDesign_v4.1.md, SystemCoreSchema.ts, SystemCoreAppendix (1).tsx, SystemCoreUXLibrary.tsx, SystemCore_v4.1_Consistency_Report.md.

## 2. Detekované nekonzistence podle vrstev
### 2.1 Data Layer (SystemCoreSchema.ts, DataModel)
- Project.yield_pa vs UX field yieldPa
  - Popis problému: rozdílné pojmenování pole mezi schema a UX (snake_case vs camelCase), chybí explicitní mapování.
  - Umístění: SystemCoreSchema.ts (Project.yield_pa), SystemCoreUXLibrary.tsx (ProjectCardProps.yieldPa).
  - Typ problému: nesoulad.
- Project.target_amount vs UX field targetAmount
  - Popis problému: schema používá target_amount, UX komponenta targetAmount bez mapovacího appendixu.
  - Umístění: SystemCoreSchema.ts (Project.target_amount), SystemCoreUXLibrary.tsx (ProjectCardProps.targetAmount).
  - Typ problému: nesoulad.
- Ticket.min_investment_amount vs UX field minInvestment
  - Popis problému: odlišné názvy pole pro minimální investici, chybí jednotné mapování.
  - Umístění: SystemCoreSchema.ts (Ticket.min_investment_amount), SystemCoreUXLibrary.tsx (TicketCardProps.minInvestment).
  - Typ problému: nesoulad.
- Ticket.duration vs UX field durationMonths
  - Popis problému: schema používá duration, UX používá durationMonths.
  - Umístění: SystemCoreSchema.ts (Ticket.duration), SystemCoreUXLibrary.tsx (TicketCardProps.durationMonths).
  - Typ problému: nesoulad.
- Ticket.max_slots vs UX field availableSlots
  - Popis problému: schema definuje max_slots, UX zobrazuje availableSlots, bez definované vazby nebo výpočtu.
  - Umístění: SystemCoreSchema.ts (Ticket.max_slots), SystemCoreUXLibrary.tsx (TicketCardProps.availableSlots).
  - Typ problému: nesoulad.
- Reservation.reservation_state vs Appendix Reservation.state
  - Popis problému: Appendix používá state a schema reservation_state, bez mapovací logiky.
  - Umístění: SystemCoreSchema.ts (Reservation.reservation_state), SystemCoreAppendix (1).tsx (Reservation.state).
  - Typ problému: nesoulad.
- Reservation.expiresAt není v schema
  - Popis problému: Appendix očekává expiresAt na Reservation, schema pole neobsahuje.
  - Umístění: SystemCoreAppendix (1).tsx (Reservation.expiresAt), SystemCoreSchema.ts (Reservation).
  - Typ problému: chybějící.
- CommissionTracking.split_percent_total vs Appendix CommissionSplit[]
  - Popis problému: schema eviduje split_percent_total, Appendix pracuje se seznamem splits bez mapování na aggregate pole.
  - Umístění: SystemCoreSchema.ts (CommissionTracking.split_percent_total), SystemCoreAppendix (1).tsx (CommissionInput.splits).
  - Typ problému: nesoulad.
- GDPRCandidate.retentionUntil/anonymizedAt vs schema retention fields
  - Popis problému: Appendix pracuje s userId/retentionUntil/anonymizedAt; schema používá data_retention_until/anonymized_at u User/Investor.
  - Umístění: SystemCoreAppendix (1).tsx (GDPRCandidate), SystemCoreSchema.ts (User.data_retention_until, Investor.anonymized_at).
  - Typ problému: nesoulad.
- AuditEvent.runId/entityId vs AuditLog/AuditMetadata
  - Popis problému: Appendix definuje AuditEvent s event/entityId/runId, schema AuditLog vyžaduje entity_type, entity_id, created_at a AuditMetadata.run_id; pole nejsou zarovnaná.
  - Umístění: SystemCoreAppendix (1).tsx (AuditEvent), SystemCoreSchema.ts (AuditLog, AuditMetadata).
  - Typ problému: nesoulad.
- Entity seznamy: Notification vs Level/Slot
  - Popis problému: DataModel uvádí Notification entity, ale schema je neobsahuje; schema obsahuje Level a Slot, ale DataModel je neuvádí.
  - Umístění: SystemCore_DataModel_v4.1.md (Entity Overview), SystemCoreSchema.ts (Level, Slot).
  - Typ problému: chybějící/duplicita.
- Relationships: Reservation → CommissionTracking (1:N) vs schema 1:1
  - Popis problému: DataModel popisuje 1:N vztah, schema má jednu CommissionTracking vazbu přes reservation_id a Relation mapuje 1:1.
  - Umístění: SystemCore_DataModel_v4.1.md (Relationships & Constraints), SystemCoreSchema.ts (CommissionTracking.reservation_id, Relations.reservation_commission).
  - Typ problému: nesoulad.
- Audit log index event_type vs schema event
  - Popis problému: DataModel používá event_type v indexech, schema definuje event.
  - Umístění: SystemCore_DataModel_v4.1.md (Indexing & Performance), SystemCoreSchema.ts (AuditLog.event).
  - Typ problému: nesoulad.
- Reservation index state vs schema reservation_state
  - Popis problému: DataModel uvádí index na state, schema definuje reservation_state.
  - Umístění: SystemCore_DataModel_v4.1.md (Indexing & Performance), SystemCoreSchema.ts (Reservation.reservation_state).
  - Typ problému: nesoulad.
- AuditLogArchive v dokumentaci vs absence ve schema
  - Popis problému: DataModel a provozní dokumenty pracují s AuditLogArchive, schema typ neobsahuje.
  - Umístění: SystemCore_DataModel_v4.1.md (Retention & Archiving), SystemCoreSchema.ts.
  - Typ problému: chybějící.
- Role seznam: Investor/DevOps vs schema User.role
  - Popis problému: dokumentace uvádí role Investor a DevOps, schema User.role je neobsahuje.
  - Umístění: SystemCore_Project_Documentation_v4.1.md (Role), SystemCoreSchema.ts (User.role).
  - Typ problému: nesoulad.

### 2.2 Logic Layer (Appendix, Governance, Validation)
- Reservation workflow: expiresAt a state vs schema reservation_state bez expiračního pole
  - Popis problému: Appendix modeluje expiraci a přechody podle expiresAt, schema pole pro expiraci nemá.
  - Umístění: SystemCoreAppendix (1).tsx (transitionReservation), SystemCoreSchema.ts (Reservation).
  - Typ problému: nesoulad.
- Commission validation logika vs schema pole
  - Popis problému: Appendix validuje sumu splitů, schema zachycuje split_percent_total bez detailu splitů.
  - Umístění: SystemCoreAppendix (1).tsx (calculateCommissionSplit), SystemCoreSchema.ts (CommissionTracking.split_percent_total).
  - Typ problému: nesoulad.
- Audit event struktura v logice vs AuditLog schema
  - Popis problému: logika pracuje s AuditEvent bez entity_type/severity/created_at, schema AuditLog je vyžaduje.
  - Umístění: SystemCoreAppendix (1).tsx (AuditEvent, notifyPendingAnonymization), SystemCoreSchema.ts (AuditLog).
  - Typ problému: nesoulad.
- Reviewer Alignment Report je uložen jako diff
  - Popis problému: soubor má formát git diff místo konsolidovaného reportu, což komplikuje referencování logických pravidel a alignmentu.
  - Umístění: SystemCore_Reviewer_Alignment_Report.md (diff hlavičky a změny).
  - Typ problému: nesoulad.

### 2.3 UX Layer (UXLibrary, UXDesign)
- UXDesign tvrdí, že UX library chybí vs existující SystemCoreUXLibrary.tsx
  - Popis problému: dokument uvádí absenci UX knihovny, ale implementační soubor je přítomen.
  - Umístění: SystemCore_UXDesign_v4.1.md (UX Architecture), SystemCoreUXLibrary.tsx.
  - Typ problému: nesoulad.
- UXDesign odkazuje na SystemCoreAppendix_Accessibility.tsx, která není v repo
  - Popis problému: přímá reference na soubor, který není dostupný.
  - Umístění: SystemCore_UXDesign_v4.1.md (Accessibility Standards).
  - Typ problému: chybějící.
- IncidentDashboard severity a SLA pole nesedí na schema
  - Popis problému: UX pracuje se severity warning/critical a slaHours, schema používá severity error/critical a sla_deadline.
  - Umístění: SystemCoreUXLibrary.tsx (IncidentDashboardProps), SystemCoreSchema.ts (SystemIncident).
  - Typ problému: nesoulad.
- CI/CD dashboard datový model chybí ve schema
  - Popis problému: UX zobrazuje CI/CD metriky (buildTimeMinutes, status), schema neobsahuje entitu pro CI/CD běhy.
  - Umístění: SystemCoreUXLibrary.tsx (CICDDashboardProps), SystemCoreSchema.ts.
  - Typ problému: chybějící.
- UX pole „status“ u ProjectCard není napojeno na omezený enum
  - Popis problému: UX používá status jako string bez enumu, schema má konkrétní enum hodnoty.
  - Umístění: SystemCoreUXLibrary.tsx (ProjectCardProps.status), SystemCoreSchema.ts (Project.status).
  - Typ problému: nesoulad.

### 2.4 Governance & Audit Layer
- SLA cíle se liší napříč dokumenty
  - Popis problému: SLA targety se rozcházejí (99.95 %, 99.98 %, 99.5 %), bez jednoho canonical KPI.
  - Umístění: SystemCore_Project_Documentation_v4.1.md (Nefunkční rozsah), SystemCore_Audit_and_Validation_v4.1.md (KPI a SLA), SystemCore_Release_and_Maintenance_v4.1.md (KPI/Summary), SystemCore_Governance_Framework_v4.1.md (SLA & Performance Metrics).
  - Typ problému: nesoulad.
- Dokumentace tvrdí chybějící schema/appendix/UX library, ale soubory existují
  - Popis problému: více dokumentů označuje tyto soubory jako chybějící, i když jsou v repo dostupné (s odlišným názvem u Appendixu).
  - Umístění: SystemCore_Project_Documentation_v4.1.md, SystemCore_DataModel_v4.1.md, SystemCore_UXDesign_v4.1.md, SystemCore_v4.1_Consistency_Report.md.
  - Typ problému: nesoulad.
- AuditLogArchive požadavek bez schematické definice
  - Popis problému: governance a data dokumenty počítají s archivací do AuditLogArchive, ale schema entitu neobsahuje.
  - Umístění: SystemCore_DataModel_v4.1.md (Retention & Archiving), SystemCoreSchema.ts.
  - Typ problému: chybějící.

### 2.5 DevOps & QA Layer
- SLA/QA KPI cíle rozdílné mezi release, audit a governance podklady
  - Popis problému: rozdílné cílové hodnoty SLA/coverage (např. 99.95 % vs 99.98 % vs 99.5 %) a coverage 97/98 % bez konsolidace.
  - Umístění: SystemCore_Release_and_Maintenance_v4.1.md (KPI pro v3.9.x), SystemCore_Audit_and_Validation_v4.1.md (KPI a SLA výsledky), SystemCore_Governance_Framework_v4.1.md (SLA & Performance Metrics).
  - Typ problému: nesoulad.
- CI/CD běhy v architektuře bez datového modelu
  - Popis problému: API /api/cicd-runs a CI/CD dashboard jsou dokumentované, ale schema neobsahuje entitu pro CI/CD běhy.
  - Umístění: SystemCore_Project_Documentation_v4.1.md (API kontrakty), SystemCoreUXLibrary.tsx (CICDDashboardProps), SystemCoreSchema.ts.
  - Typ problému: chybějící.

## 3. Souhrnná tabulka
| Vrstva | Typ problému | Soubor | Sekce | Status |
| --- | --- | --- | --- | --- |
| Data | Field mismatch | SystemCoreSchema.ts / SystemCoreUXLibrary.tsx | Project.yield_pa vs ProjectCard.yieldPa | ⚠️ |
| Data | Missing entity | SystemCoreSchema.ts | Notification entity | ⚠️ |
| Data | Relationship mismatch | SystemCore_DataModel_v4.1.md | Reservation → CommissionTracking (1:N) | ⚠️ |
| Logic | Audit event schema mismatch | SystemCoreAppendix (1).tsx | AuditEvent vs AuditLog | ⚠️ |
| UX | Missing mapping | SystemCoreUXLibrary.tsx | TicketCard availableSlots vs max_slots | ⚠️ |
| UX | Severity mismatch | SystemCoreUXLibrary.tsx | IncidentDashboard severity vs SystemIncident | ⚠️ |
| Governance | KPI discrepancy | SystemCore_Governance_Framework_v4.1.md | SLA & Performance Metrics | ⚠️ |
| QA | SLA target mismatch | SystemCore_Audit_and_Validation_v4.1.md | KPI a SLA výsledky | ⚠️ |

## 4. Závěr
Audit identifikoval opakované nesoulady v pojmenování polí, rozdílné definice KPI/SLA a chybějící vazby mezi schema, appendixy a UX knihovnou. Závažnost je zvýšená zejména u datových mapování, auditních eventů a governance metrik, které brání jednoznačné referenci na canonical zdroje pravdy.
