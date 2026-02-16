# Oracle Pluggable Database (PDB) Management Assignment

## 📋 Student Information
- **Name:** Mwizere Kisa Sabin
- **Student ID:** 28408
- **Course:** Database Development with PL/SQL (INSY 8311)
- **Instructor:** Eric Maniraguha
- **Assignment Date:** February 15, 2026
- **Submission Deadline:** February 16, 2026

## 💻 Oracle Environment
| Component | Details |
|-----------|---------|
| **Oracle Version** | Oracle Database 21c Enterprise Edition 21.3.0.0.0 |
| **Operating System** | Microsoft Windows x86 64-bit |
| **Container DB Name** | ORCL21C |
| **OEM Port** | 5500 |
| **PDB Seed Location** | C:\ORCL\ORADATA\ORCL21C\PDBSEED\ |

---

## 📁 Task 1: Create Permanent PDB

### PDB Details
| Parameter | Value |
|-----------|-------|
| **PDB Name** | `er_pdb_2024101` |
| **Admin Username** | `eric_plsqlacua_2024101` |
| **Password** | `SimplePass123` |
| **Creation Date** | February 13, 2026 |

<img width="322" height="97" alt="database deleted" src="https://github.com/user-attachments/assets/bcd16489-f7a9-4f1a-947a-aa53eeb02a73" />
<img width="350" height="176" alt="database exist" src="https://github.com/user-attachments/assets/0e69c7b8-59de-41ba-9de4-47f3adf66a2d" />


<img width="314" height="163" alt="plugable database " src="https://github.com/user-attachments/assets/e673ef65-7251-493c-bf4c-861bb9b0674c" />



<img width="839" height="524" alt="cdb dashbrood" src="https://github.com/user-attachments/assets/126d0ead-d12f-478b-ad5e-f5489f1d682a" />



-- Create PDB
SQL> CREATE PLUGGABLE DATABASE er_pdb_2024101
  2  ADMIN USER eric_plsqlacua_2024101 IDENTIFIED BY 'SimplePass123'
  3  FILE_NAME_CONVERT = ('C:\ORCL\ORA14\ORCL12\ORBSERVER', 
                         'C:\ORCL\ORA14\ORCL12\ORBSERVER');

Pluggable database created.

-- Open PDB
SQL> ALTER PLUGGABLE DATABASE er_pdb_2024101 OPEN;

Pluggable database altered.

-- Verify PDB is open
SQL> SELECT name, open_mode FROM v$pdbs WHERE name = 'ER_PDB_2024101';

NAME           OPEN_MODE
-------------- ----------
ER_PDB_2024101 READ WRITE

-- Create temporary PDB
SQL> CREATE PLUGGABLE DATABASE er_to_delete_pdb_2024101
  2  ADMIN USER temp_admin IDENTIFIED BY 'TempPass123'
  3  FILE_NAME_CONVERT = ('C:\ORCL\ORA14\ORCL12\ORBSERVER',
                         'C:\ORCL\ORA14\ORCL12\ORBSERVER');

Pluggable database created.

-- Open temp PDB
SQL> ALTER PLUGGABLE DATABASE er_to_delete_pdb_2024101 OPEN;

Pluggable database altered.

-- Delete temp PDB
SQL> ALTER PLUGGABLE DATABASE er_to_delete_pdb_2024101 CLOSE IMMEDIATE;
SQL> DROP PLUGGABLE DATABASE er_to_delete_pdb_2024101 INCLUDING DATAFILES;

Pluggable database dropped.

-- Verify deletion
SQL> SELECT name FROM v$pdbs WHERE name = 'ER_TO_DELETE_PDB_2024101';

no rows selected

-- Check OEM port
SQL> SELECT dbms_xdb_config.gethttpsport FROM dual;

GETHTTPPSPORT
-------------
         5500
         
