# Pre-Requisites
1) SubAccount - Entitlements
- Authorization and Trust Management Service
- Build Work Zone, standard edition
2) Service Marketplace subscription 
- SAP BAS with roles
- SAP HANA Cloud (tools option) with roles
- **Note:** if Not found, subscribe from Service Market place

# HANA DB Instance
1. SubAccount - HANA Cloud - Create - HANA DB Instance created.
2. Start & open HANA Database explorer - HANA DB instance is there
3. Import catalog data (sflight_hana.tar.gz)
4. Go to table - slect SFlight - open any Table data 

# HANA DB User/Roles setup
1. SAP HANA Cloud Central - Expand DB Instance
2. Go to User & Authorization Management - Roles
3. Create roles (User Management) & Users (Role Management)
4. In existing roles assign, SFLIGH Schema (Objects with Privileges) & users.

# Query the Database Using SQL Statements
1. To set any schmea, run query as 'SET SCHEMA SFLIGHT'
2. copy existing table to new table and check
3. CREATE TABLE SAGENCYDATA as (select SBOOK.AGENCYNUM, count(SBOOK.AGENCYNUM) as NUMBOOKINGS FROM SBOOK, STRAVELAG WHERE SBOOK.AGENCYNUM=STRAVELAG.AGENCYNUM group by SBOOK.AGENCYNUM ORDER BY count(SBOOK.AGENCYNUM) desc)
4. SELECT * FROM SAGENCYDATA;
5. Join the tables, SELECT TOP 5 SAGENCYDATA.AGENCYNUM, STRAVELAG.NAME,SAGENCYDATA.NUMBOOKINGS FROM SAGENCYDATA INNER JOIN STRAVELAG on SAGENCYDATA.AGENCYNUM = STRAVELAG.AGENCYNUM;



