# COMPLETE VERSION IN ENGLISH

## Phase 1: Individual Work

### a) PHASE 1 POL

**What will we back up?**  
- **Databases:** critical data used daily.  
- **Project Documents:** containing plans and important technical specifications.  
- **User Document folders:** may contain important work information.  

> Note: It is not necessary to back up all users’ personal files on client computers, only the “Documents” folders, to avoid unnecessary temporary or personal files.

**How often and in what way?**  
- **Databases:** Incremental backups every 4 hours (4-hour RPO), full backup weekly.  
- **Project Documents & Personal Folders:** Daily differential backup, weekly full backup.  
- **Client computers (Documents folders):** Daily incremental backup or synchronization.

**What media to use and where to store data**  
- **Local:** NAS (fast, local access)  
- **External:** Cloud (Azure, Google Cloud, or local service)  
- **External disks:** SSDs, HDDs, tapes for monthly/weekly backups  

**3-2-1 Rule:**  
3 copies, 2 different types of media (NAS + Cloud), 1 copy offsite (Cloud)

---

### b) PHASE 1 XAVI

**Data to Back Up (Prioritization)**  
| Data | Size | Notes |
|------|------|------|
| Databases (Accounting and Clients) | 20 GB | Critical, used daily |
| Project Documents | 300 GB | Important, moderate growth, 24h RPO |
| Personal Folders | 100 GB | Necessary for daily work, less critical |
| Client Computers (Windows 10/11) | - | Only local Documents folders need backup |

**Frequency and Type of Backup**  
- **Databases:** Incremental every 4h, full daily  
- **Project Documents:** Incremental daily, full weekly  
- **Personal Folders:** Incremental daily, full weekly  
- **History:** Minimum retention 1 month → weekly/monthly archived backups

**Media and Location (3-2-1 Rule)**  
- **Local NAS:** fast backups, immediate restoration  
- **Cloud:** offsite backup  
- **External disks:** archived weekly/monthly backups  

**3-2-1 Rule:**  
- 3 copies (original + 2 backups)  
- 2 types of media (NAS + Cloud)  
- 1 copy offsite  

> Important: Most recent backup should be local (NAS) for quick restoration, replica in Cloud for disaster protection.

---

### c) PHASE 1 BLAI

**What will we back up?**  
- Critical server data: databases (clients/invoices), shared documents/projects, server configurations (accounts/permissions), VMs, important logs.  
- Only back up client computers with unique local files or difficult-to-reproduce configurations.

**How often and in what way?**  
- **Every working day:** Incremental backup (changes since last backup)  
- **Weekly (Saturday):** Differential backup (all changes since last full backup)  
- **Monthly:** Full backup of all critical server data

**Media and Location**  
- External hard drives, NAS, Cloud, tapes  
- Follow 3-2-1 rule: original on server, copy on NAS/external disk, copy offsite (Cloud)

---

### d) PHASE 1 PAU

**Backup Report**  
- Critical server data: project documents, Accounting and Clients database, users’ personal folders  
- Client computers: only folders with temporary important files  
- **Backup Types:**  
  - Daily incremental for Accounting/Clients  
  - Weekly full backup of server  
  - Daily differential for documentation & personal folders  
  - Monthly full backup for all data  
- **Backup Medium:** NAS (centralized, fast), extra copy in Cloud  

---

## PHASE 2: Work in couples

### Pol & Pau

**1. Discussion and Consensus**  
- Agreed on critical data to store  
- Only “Documents” folders backed up, not all personal files  
- Frequency: some differences, but backup type agreed  

**2. Unified Proposal (3-2-1 Backup Scheme)**  

| Element | Couple’s Proposal | Justification |
|---------|-----------------|---------------|
| Critical Data | Project Documents, Accounting/Clients DB, Personal Folders | Essential for daily operations |
| Frequency (Databases) | Daily | Recovery of recent changes |
| Backup Type (Databases) | Daily incremental, weekly full | Incremental = speed; full = stability |
| Media 1 (Local) | NAS | Fast recovery in office |
| Media 2 (External) | Cloud | Offsite recovery (3-2-1 rule) |

---

### Xavi & Blai

**1. Discussion and Consensus**  

| Aspect | Xavi | Blai | Similarities / Differences |
|--------|------|------|---------------------------|
| What to back up | Databases, project documents, personal folders | Databases, documents, server config, accounts, permissions, VMs, logs | Agree not to backup all clients. Xavi focuses on daily data; Blai includes config/logs |
| Frequency | Databases: incremental 4h + daily full; Docs/folders: daily incremental + weekly full | Daily incremental M–F, weekly differential Sat, monthly full | Xavi meets 4h RPO; Blai uses standard scheme |
| Backup type | Incremental + full | Incremental + differential + full | Xavi adapts to RPO/RTO; Blai standard scheme |
| Media & location | NAS + Cloud + external disks | External disks + NAS + Cloud + tapes | Xavi practical; Blai adds long-term storage |

**2. Unified Proposal (3-2-1 Backup Scheme)**  

| Element | Proposal | Justification |
|---------|---------|---------------|
| Critical Data | Accounting/Clients DB, Project Docs, Personal Folders | Essential for daily operations; databases have strict RPO/RTO |
| Frequency (Databases) | Incremental every 4h + daily full | No more than 4h data loss; quick restoration |
| Backup Type (Databases) | Incremental + Full | Fast incrementals; solid restore points |
| Media 1 (Local) | NAS | Immediate access & fast restoration |
| Media 2 (External) | Cloud | Protection against physical disasters; remote availability |

---

## Phase 3: Group Work

**Discussion and Selection**  
- Both plans prioritize critical data (databases, project docs, personal folders)  
- Pol & Pau: simpler, easier daily management, cost-effective  
- Xavi & Blai: aligns with RPO/RTO, long-term options, media diversity; more robust but complex

**Final Backup Policy for Muntatges i Serveis Tècnics SL**  
- Critical data: project documents, Accounting/Clients database, users’ personal folders  
- **Backup Schedule:**  
  - Accounting/Clients: daily incremental, weekly full  
  - Documentation & personal folders: daily differential, monthly full  
- **Media:** NAS (local, fast), Cloud (offsite)  
- Policy ensures availability, security, and meets company requirements

---

## Final Document (Phase 3)

### 1) Data to be Backed Up

**Server**  

| Data Type | Critical | Backup Frequency |
|-----------|---------|----------------|
| Databases (Accounting/Clients) | ✅ | Incremental every 4h + daily full |
| Project Documents | ✅ | Daily incremental + weekly full |
| Users’ Personal Folders | ❌ | Daily incremental + weekly full |

**Client Machines**  

| Data Type | Critical | Backup Frequency |
|-----------|---------|----------------|
| Temporary local documents | ❌ | Not backed up (recommend saving on server) |
| Special configurations | ✅ (if any) | Occasional backup if difficult to recover |

**Summary**  

- **Server:**  
  - Critical: Accounting/Client DBs, Project Docs → daily incremental, weekly full, monthly full  
  - Non-Critical: Personal Folders → daily differential, monthly full  
- **Clients:**  
  - Critical: key technician folders → daily differential, monthly full  
  - Non-Critical: other files not backed up

---

### 2) Detailed Weekly Schedule

| Day | Data | Backup Type | Medium |
|-----|------|------------|--------|
| Monday | Accounting/Clients, Project Docs | Incremental | NAS |
| Monday | Users’ personal folders | Differential | NAS |
| Tuesday | Accounting/Clients, Project Docs | Incremental | NAS |
| Tuesday | Users’ personal folders | Differential | NAS |
| Wednesday | Accounting/Clients, Project Docs | Incremental | NAS |
| Wednesday | Users’ personal folders | Differential | NAS |
| Thursday | Accounting/Clients, Project Docs | Incremental | NAS |
| Thursday | Users’ personal folders | Differential | NAS |
| Friday | Accounting/Clients, Project Docs | Incremental | NAS |
| Friday | Users’ personal folders | Differential | NAS |
| Saturday | Accounting/Clients, Project Docs | Incremental | NAS |
| Saturday | Users’ personal folders | Differential | NAS |
| Sunday | Full backup of entire server & client data | Full | NAS + Cloud |

---

### 3) Choice of Media and Location (3-2-1 Rule)

- **Medium 1 (Local):** NAS located in office, centralized, fast recovery  
- **Medium 2 (External):** Cloud (Azure or Google Cloud), offsite backup, high availability  
- **Offsite Location:** Cloud managed by service provider, supervised by admin

---

### 4) Recovery Strategy (RTO/RPO)

- **RPO:** Daily incremental backups ensure no more than 4h of data loss for Accounting/Clients  
- **RTO:** Recovery from local NAS for immediate access; Cloud backup used if NAS unavailable  
- Ensures quick restoration and minimal impact on business operations

👉 [Torna a la pàguina de la tasca](README.md)  
📍 [Torna a la pàguina del projecte](../../README.md)
