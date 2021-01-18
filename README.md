# SpringbootVault
This is a Spring boot project that does CRUD operations in a MySql DB. It uses Spring data to connect to the DB. The DB credentials are stored in Hashi corp Vault.
To set up database run below query the MySql workbench.

CREATE TABLE `product` (
  `name` varchar(30) NOT NULL,
  `quantity` int(11) NOT NULL,
  `id` bigint(20) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='product table';


In order to set up the vault, download it from https://www.vaultproject.io/downloads site.
Unzip the exe, then using the CMD ( assume Windows machine) run below command. 

vault server --dev --dev-root-token-id="00000000-0000-0000-0000-000000000000"

This will start the vault server by default in 8200 port, with a token id to identify the serveer instance. Then open another command prompt and run

vault kv put secret/gs-vault-config db.userName=<user name> db.password=<password> db.url=jdbc:mysql://localhost:3306/product_db?serverTimezone=UTC

This will create a vault entry under 'gs-vault-config' and stores database userame, password and URL. I haven't edited the DB URL, so that reader can understand the URL pattern.

Here we use Spring cloud for vault integration. The dependencies can be found in the the pom.xml.

Finally run the application as a Java application.
