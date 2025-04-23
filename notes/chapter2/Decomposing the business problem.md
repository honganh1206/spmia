The architect breaks the business problem into chunks representing discrete domains of activity

Sometimes groups of microservices need to complete an entire transactions, and the architect's job is to look at where the data domain does not seem to fit together

![[Pasted image 20250422174824.png]]

An existing application may have hundreds of tables, but each table will usually map back to a single set of logical entities

![[Pasted image 20250423143124.png]]

Four microservice candidates: Organization, license, contract and assets services