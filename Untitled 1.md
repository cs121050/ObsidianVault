

```yml
spring:

datasource:

url: jdbc:sqlserver://localhost:1433;encrypt=true;trustServerCertificate=true;databaseName=JazzLibraryHibernate # SQL Server connection URL

username: sa # Database username

password: A123!@#alepasas # Database password

driver-class-name: com.microsoft.sqlserver.jdbc.SQLServerDriver # JDBC driver for SQL Server

  

jpa:

show-sql: true # Log SQL statements to console

open-in-view: false # Disable Open Session In View pattern (prevents session issues)

hibernate:

ddl-auto: create # Drop and recreate schema on startup (also: create, update, validate, none)

naming:

physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl # Use exact column names without modification

defer-datasource-initialization: true # Run data.sql AFTER Hibernate creates tables, that initialises the db

properties:

hibernate:

format_sql: true # Format SQL output for better readability

use_sql_comments: true # Include comments in generated SQL

  

sql:

init:

mode: always # Always run data.sql on startup (options: always, embedded, never)

platform: sqlserver # Use data-sqlserver.sql if it exists (optional)

continue-on-error: false # Stop application if SQL errors occur during initialization

  

transaction:

default-timeout: 90 # Transaction timeout in seconds

rollback-on-commit-failure: true # Rollback transaction if commit fails

  

server:

port: 8080 # HTTP server port
```