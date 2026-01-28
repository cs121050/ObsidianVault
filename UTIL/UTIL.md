


HOW To make a repo in github and accesse it in IDE!

HOW to clone a repo, and access it in IDE 

### Install python
`winget install --id Python.Python.3.13 -e`
if doesnt exist , you need to find a stable version , run this to find it 
`winget search python`



## Branching strategy

#todo : consider to make a preprod repository ... and create aproper burncing strategy ,, so pushing on the production all the time,, production need to have valid code at all times....



### Characters that crashing POSTGRE db whle using in strings

Characters that crashing POSTGRE db whle using in strings in a string entity,, they need to be removed, the previus bat files i made was crap #todo make new bat files to hanle it
lol

1. first of all you need to convert your sql to postgre-sql
2. ```txt
   you need to remove '--', '\', ';' 
   '--': open comments and creeps out the commands
   '\': 
    ';' : postgre things its the end of line, once upon a time those characters was upostrofes or somethingelse
   ```




### Vocabulary 
- `dev` → running on your laptop
- `prod` → running on Railway (real internet users)
- `test` → automated tests

Yaml: Always use **spaces, not tabs**


## AI Prompts



**ECLIPSE**
**ctrl-H** find txt in all project!






### Deploy repo to Railway (HostApp)

Go to https://railway.com/account / login with GitHub / click the profile icon, click settings, acount integrations, github, configure :: now railway can see your repos / new project, deploy your repo / Now you need a DB, click new, new database, **PostgreSQL(Best match with SpringBootApi)** / click the SpringBootApi, go to Variables, add dbUrl dbuser dbpassword from postgre variables, allso add another varioable with name: SPRING_PROFILES_ACTIVE and value: 'prod' , press **DEPLOY** / now you need to go to you api code in IDE, at application.properties, and add the variables you just created in it, 
```java
server.port=${PORT:8080}

spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false
```
	at this point i added 'profiles' in my project: aplication.yaml aplication-prod.yaml aplication-dev.yaml, i had to add the aplication-dev.yaml to .gitignore because it was contqaining the credentials of my local db. Those are the .yaml files after the change.

aplication.yaml 
```yaml
spring:
  profiles:
    active: dev # Default profile for local development
```

aplication-prod.yaml
```yaml
spring:

datasource:

url: jdbc:sqlserver://localhost:1433;encrypt=true;trustServerCertificate=true;databaseName=jazzLibraryDB

username: sa

password: A123!@#alepasas

driver-class-name: com.microsoft.sqlserver.jdbc.SQLServerDriver

  

jpa:

show-sql: true

open-in-view: false

hibernate:

ddl-auto: update

naming:

physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl

  

server:

port: 8080
```

aplication-dev.yaml
```yaml
spring:

datasource:

url: ${DB_URL} #railway provides the database url as an environment variable

username: ${DB_USERNAME}

password: ${DB_PASSWORD}

driver-class-name: org.postgresql.Driver

  

jpa:

hibernate:

ddl-auto: validate

naming:

physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl

show-sql: false

open-in-view: false

  

server:

port: ${PORT:8080} #tells railway to use its assigned port or default to 8080, railway is a cloud platform that i have my api deployed on.
```

put this , or any change in a new branch, add,comit,push, make new PR, merge it to main, // 
once the springput api is running after deploy, go to settings and 'generate domain'/ tHE API is now online! open Postman and test it!! Although yuou will not be able to retreave data once the DB is yet empty, you now nee to populate it... // for that you will need a 'postman app' but for testing and innitialising the remote online postgre DB! Download//install DBeaver // new database connectyion, postgre , maintab, connect by Host, fill the entries deconstructiong the public URL you will find at // in rail2way open the DB service , goto databaseTab, connect , publick network, coppy the URL, decontruct it to get from it, USERNAME, password, database name port, host// paste those in DBeaver fields, test connection, enable SSL and mark is as 'required' // use the .bat to trAnslate the microsoft sql to postgre, and populate,, test with post man 




PGPASSWORD=PviunIxYXtXoDGQbAZtSqSBayDFSDavx psql -h switchyard.proxy.rlwy.net -U postgres -p 25371 -d railway




### Logging App  (Splunk like app)

@level:info , @level:error, @level:warn 








## clone repo in source tree



## make a PR...

include testing, after deployment...




## Take aways of geting FIRED






## Obsidian syntax

**Bold**
*Italic*
***Bold + Italic***
~~Strikethrough~~  ~~ ~~
`Inline code`

```
# H1
## H2
### H3
#### H4
```

- Item
- Item
  - Sub-item
- [ ] To do
- [x] Done

- [ ] Practice
  - [ ] Warm-up
  - [ ] Transcription

[[My Note]]

[[My Note|Readable Name]]

[YouTube](https://youtube.com)

#jazz
#practice/guitar


> This is a quote
>> Nested quote


> [!tip]
> [!warning]
> [!info]
> [!quote]
> [!example]



> [!note]- Collapsed title
> Hidden content



```java
System.out.println("Hello");
```


| Tune | Key | Tempo |
|-----|----|------|
| All The Things You Are | Ab | Medium |
| Blue Bossa | Cm | Latin |




![[image.png|300]]




![Alt text](https://example.com/image.png)


![[My Note]]


This is a paragraph ^blockid

==Highlighted text==



## Run the .bat file to convert sql sql to postgre sql

```bash

 C:\Users\User\Desktop\ha.bat "C:\Users\User\Desktop\Jazz library PostGre initialiasation.txt"
 
 
```


---



## Android Terminal

```bash
#open terminal
./gradlew clean 
./gradlew build
```
 **Lesson 1: Version Management is Critical**

Android development has **four layers** that must be compatible:

1. **Android Gradle Plugin (AGP)** - The build system (your `agp = "8.6.1"`)
    
2. **Compile SDK** - The Android API level you compile against (`compileSdk = 34`)
    
3. **Dependency versions** - The libraries you use
    
4. **Kotlin version** - The language compiler
    

**Rule of thumb:** When creating a new project, use slightly older, stable versions.


**Enable Auto-Save in Android Studio:**

- **File** → **Settings** → **Appearance & Behavior** → **System Settings**
    
- Check: **✓ Save files on frame deactivation**
    
- Check: **✓ Save files automatically if application is idle for ___ sec** (set to 15)
    
- **Apply** and **OK**