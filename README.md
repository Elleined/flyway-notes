# flyway-notes
Notes for Flyway an open source tool for managing you database migrations

# Current Problem before using flyway
- Most software applications use SQL databases on account of their reliability, consistency, and maturity when it comes to handling structured data. The database schema evolves over time as business requirements change to add new features or update existing ones.

- Object-relational mapping (ORM) frameworks like JPA/Hibernate provide an easy way to generate a database schema based on JPA entities, which can be convenient during development. For example, while using Spring Data JPA, you can configure the property spring.jpa.hibernate.ddl-auto=update to automatically create or update tables based on JPA entities.

- However, automatically updating the database schema based on JPA entity changes is risky and error-prone, especially in production environments. Instead, it is recommended to use a database migration tool like Flyway.

# Flyway features
- Automated Schema Changes
- Version Control for your Database
- Consistency Accross Environments
- Easy Rollbacks
- Supports multiple Databases

# What is Flyway
[Flyway tutorial](https://blog.jetbrains.com/idea/2024/11/how-to-use-flyway-for-database-migrations-in-spring-boot-applications/)
- Flyway is an open-source database migration tool that simplifies the process of managing and versioning database schema changes. 

- With Flyway, migration scripts are stored alongside application code, following a consistent, versioned approach that allows teams to manage database changes as part of their regular development workflow. Flyway supports a wide range of databases, including MySQL, PostgreSQL, Oracle, SQL Server, and many others.

- Flyway uses a simple versioning system to manage migration scripts. Each script is assigned a unique version number (e.g. V1__init.sql, V2__create_articles_table.sql), which Flyway uses to track which scripts have been applied and which are pending.

- The naming convention for versioned migrations is:{Prefix}{Version}{Separator}{Description}{Suffix}

- By default, for versioned migrations, {Prefix} is V, {Separator} is __, and {Suffix} is .sql.

- Any changes in database schema is considered as migration
- Open-source
- Database Migration Tool
- Makes easy to manage DB Schema
- Integrates with Spring Boot
- Support wide range of DB
# 2 Types of migration
- Versioned Migration
	- Most common type of migration
	- Applied once in order they appear.
	- Used for creating, altering, dropping table, indexes, and foreign keys
	- with naming convention of V1_ _ add_user_table.sql
		- V1: Prefix
		- _ _ : Separator
		- add_user_table: Migration file name
		- .sql: Suffix

- Repeatable Migration
	- Reapplied every time there are checksum changes.
	- Used for managing views, stored procedures, or bulk reference data updates.
	- Applied after all versioned migration are applied.
	- with naming convention of R _ _ create_user_view.sql
		- R: Prefix
		- _ _ : Separator
		- add_user_table: Migration file name
		- .sql: Suffix

# Execution
- So it will run first the Version migration in order they appear and then run the Repeatable migrations

# Flyway Spring boot dependencies
- core
- vendor specific driver  
Example in Spring boot that uses MySQL
```
<dependency>
			<groupId>org.flywaydb</groupId>
			<artifactId>flyway-core</artifactId>
		</dependency>
		<dependency>
			<groupId>org.flywaydb</groupId>
			<artifactId>flyway-mysql</artifactId>
		</dependency>
```

# Flyway application.properties
```
# Flyway
spring.flyway.enabled=true
spring.flyway.validate-on-migrate=true
spring.flyway.baseline-on-migrate = true
spring.flyway.baseline-version = 0
```
