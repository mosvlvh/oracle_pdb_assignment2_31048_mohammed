# Oracle Multitenant Architecture & PDB Management Assignment

## 1. Assignment Overview
This assignment demonstrates practical database administration skills using Oracle Multitenant Architecture. It includes creating and configuring Pluggable Databases (PDBs), managing local database users, handling temporary PDB life-cycles, and documenting technical workflows using version control platforms.

---

## 2. Oracle Environment
* **Oracle Database Version:** Oracle AI Database 26ai Free Release (Version 23.26.2.0.0)
* **Operating System:** Manjaro Linux (KDE Plasma Desktop Environment)
* **Tools Used:** Oracle SQLcl (Release 25.4), Zen Browser

---

## 3. Task Documentation

### Task 1: Create and Configure a New PDB
* Successfully navigated to the `CDB$ROOT` container to instantiate the pluggable database.
* Created `mo_pdb_31048_2025` using explicit path file transformations for the Oracle Free directory tree.
* Switched sessions to the new container, provisioned the local administrative user `mohammed_plsqlauca_31048_2025` with password authorization, and granted `CONNECT`, `RESOURCE`, and `DBA` privileges.
* Verified direct structural endpoint login via network thin-clients.

### Task 2: Create and Delete a Temporary PDB
* Created a temporary pluggable clone named `mo_to_delete_pdb_31048_2025`.
* Validated its registration status, safely brought it online, immediately isolated its active states via `CLOSE IMMEDIATE`, and permanently removed it along with all physical storage blocks utilizing the `INCLUDING DATAFILES` clause.

### Task 3: OEM Configuration & Technical Justification
**Important Notice regarding Oracle Enterprise Manager Configuration:**
Due to working under a modernized ecosystem utilizing **Oracle AI Database 26ai Free / 23c Free on Linux**, the legacy browser-based Oracle Enterprise Manager Express (EM Express) typically found on port 5500 has been completely deprecated and stripped down by Oracle Corporation in favor of the new Oracle Database Actions framework. 

I have spent an extensive amount of time and effort attempting to manually force compile the legacy `XDB` configurations, open persistent system dispatchers, and mapping loopback connection paths on port 5500 via my web browser. Unfortunately, the server engine fundamentally rejected standard OEM interfaces due to this architectural omission in the new release. 

As an alternative engineering validation, I have provided command-line programmatic evidence showing an active and successful query of the database Instance, full structural version profiles, and online `READ WRITE` operational states of the assigned PDBs to confirm an identical, stable administrative backend.

---

## 4. Challenges and Solutions
1. **Container Privilege Violations (`ORA-65040`):** Encounted when running PDB creations from internal local containers. Resolved by explicitly reverting connection states to the root wrapper context using `ALTER SESSION SET CONTAINER = CDB$ROOT`.
2. **Directory Mapping Failures (`ORA-65005`):** Standard default installation file converts did not align with Oracle Free structural roots on Linux. Remedied by tracking the correct installation nodes under `/opt/oracle/oradata/FREE/pdbseed/` and updating path parameters.
3. **JDBC Unauthenticated Logins (`ORA-01017`):** Direct host stringless authentications fail on network-driven toolchains like SQLcl. Fixed by supplying explicit secure remote identifiers (`sys/mo88@//localhost:1521/FREE as sysdba`).

---

## 5. Lessons Learned
* Deep understanding of Oracle's Multitenant Architecture, handling root containers versus pluggable databases.
* Mastering clean instance teardowns and memory data-file purging strategies via structural drops.
* Troubleshooting system network dispatchers, environment variable bindings, and diagnosing versioning differences across modern enterprise systems.

---

## 6. Integrity Statement
"I confirm that this assignment represents my own practical work, screenshots, and documentation. All external resources consulted have been properly acknowledged."
