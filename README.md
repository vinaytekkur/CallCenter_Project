# Call Center Project
Complete ETL data pipeline with business logic execution of one of Call Center using Azure.

**Bussiness Statement/Requirement:**
Call Center "XYZ" wants to build complete end-to-end solution for it's handling daily calls agent makes to customer. As call center agent some people might be abset during some occasions or due to some personal  emergency, Hence company looking for complete solution to handle the case with automation approach
1) Every day Call center will upload file which includes that days present list of call center agents.
2) We should create bussiness logic which analyses data in the file and dynamically allocates respective customers.
   Note: Accounts or customers should be allocated to Call center based on position (i.e first preference should be "Seniors" and after all accounts allocation of Seniors it should pick "Juniors")
3) While allocating accounts to call center agent - each call center agent should get equal number of call (i.e : if person A allocated 3 calls then person B should also allocate 3 calls).
4) Allocating accounts should be based on purchases made customer (i.e: Customer who purchased highest number of products should be prioritize first)

**Architechture:**
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/b5482fcc-37b7-4598-b70f-38398fcf62e9)

**Services/Tools/Languages Used:**
1) Azure Data Factory (Pipeline creation and orchestration)
2) Azure Key Vault (Securing credentials)
3) Azure Service Principle
4) Azure GEN2 blob storage
5) SQL Server
6) SQL (MS SQL) - Stored Procedure for building business logic 

**Sources:**
1) Call Center uploads daily file(.csv) which contains that day call center agent data.
2) SQL Server which contains sales information and other respective tables needed for analysis.

**Ingestion Layer:**
1) Using Data Factory - Take data from source and put those data into respective sink (destination)

**Transformation Layer:**
1) In this will execute actual logic based on bussiness requirement(Used Stored Procedure)

**Publish Layer:**
1) Final data will be updated into SQL server - using stored procedure

Pipeline data designed based on daily execution status - it takes data dynamically picking respective folder from Gen2 storage and executing respective logic. Also will receive Email Notification if pipeline executed successfully or failed.

**Source Data:**
Call Center Sales data DB architechture:
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/e637f44c-e3f2-450c-ba4f-e512d2ca0797)

**Step 1:**
1) We need to merge required data from different dimentional tables to get final dataset - Hence we created Stored Procedure which merges all respective data into one table by dynamically selecting dates.
2) Copy activity responsible for moving Call Center Agent information into SQL table (Gen 2 to SQL server data movement)
3) Final Stored Procedure will rank customers based on purchases made also ranks Call Center agent based on Position (Senior should be first priority and then Juniors)

**Step 2:**
1) Execute Business Logic - Based on customers priority dynamically assign respective Call Center Agent
2) Example: On 5th Feb in csv file we received total 4 Call Center Agents
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/6ceeca4b-9577-452a-a62b-c7a1df99ff33)

Using Stored Procedure prioritized respective customers:
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/ac7bf278-0e28-408f-b7f6-4726699fb63b)
Criteria based on number of purchases made

Hence There are totally 11 customers and 4 Call center agents
Then Each Call Center Agent will get 3 Accounts, Final result will be pushed into SQL server after executing stored procedure.

**Final Result Set:**
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/8db1a735-b74b-4200-bb69-018d9e0fe5cb)
Every Call Center agent assigned 3 accounts - Seniors assigned high prioritized accounts and after allocating them next turn with Juniors.

**Final Data Factory pipeline:**
![image](https://github.com/vinaytekkur/CallCenter_Project/assets/156997918/28a1b341-357d-4961-89c1-1b7599e098bf)

Enjoyed doing this project - SQL server, Data insertions, Data pipeline design and writing logic everything implemented from scratch :)
Thanks, Have a great day!!



