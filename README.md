# Liquibase Node.js Example
Forked from https://github.com/tabuckner/node-liquibase-sandbox 

# Usage
Install necessary dependencies
```bash
npm i
```
The MySQL connector is bundled in the `./lib` folder, but there are binaries for Liqubase in the ./node_modules/node-liquibase/dist/drivers folder (postgresql, mariadb, etc.)

Start the database
```bash
docker compose up #or 'docker-compose up' if you have an older version of docker
```

Run the migrations
```bash
npm run node-liquibase -- --changeLogFile="changelog.xml" --url="jdbc:mysql://localhost:3306/node_liquibase_testing" --username="yourusername" --password="yoursecurepassword"  --classpath="./lib/mysql-connector-j-9.0.0.jar" update
```

Now the database should have a table called `execSales123` with 3 columns.

Rollback the last 1 migration
```bash
npm run node-liquibase -- --changeLogFile="changelog.xml" --url="jdbc:mysql://localhost:3306/node_liquibase_testing" --username="yourusername" --password="yoursecurepassword"  --classpath="./lib/mysql-connector-j-9.0.0.jar" rollbackCount 1
```

The database should now have a table called `execSales123` with 2 columns (address column migration was rolled back).

# Notes
- The `changelog.xml` file is the file that contains the migrations. It is a standard Liquibase file. I tried to use YAML format for the changelog but there was an error: `Unexpected error running Liquibase: Multiple nodes match null/name`
- This changelog format is the compact version. In reality there would be a [master changelog](https://docs.liquibase.com/concepts/changelogs/home.html) file that includes all the other changelogs.