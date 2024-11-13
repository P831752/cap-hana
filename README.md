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

# MyHANAApp Application - Combine CAP with SAP HANA Cloud to Create Full-Stack Applications
0 https://developers.sap.com/mission.hana-cloud-cap.html
1. CAP Project with Choose **Node.js** as the runtime. Select **SAP HANA Cloud** from the database for your application section. Choose **Cloud Foundry:MTA Deployment** and **CI/CD Pipeline Integration** under which way to deploy your project. Choose SAP **BTP Authorization** and **Trust Management Service (XSUAA)** and **SAP Application Router**
2. Run, npm i & npm install -g hana-cli & hana-cli version
3. Define **db**, **header** & **items** entities with **Comoposition** & **association** relation ship
4. **Bind** HANA DB from **SAP HANA Projects** and create **New Service Instance** 
5. check **cf services** able to see hana services
6. **Deploy** (Rockt symbol) initial artifacts.
7 Run **cds bind -2 MyHANAApp-dev:SharedDevKey** cdsrc-private.json created (CAP srv to HANA connection)
8. cds compile srv/ --to xsuaa > xs-security.json
9. cf create-service xsuaa application MyHANAApp-auth -c xs-security.json
10.cds bind -2 MyHANAApp-auth:default
11.cds bind --exec -- npm start --prefix app/router **(not working)**
12. cds watch --profile hybrid
