# SFDC-CLI-Changeset-Validator
Ant & SFDC migration tool based CLI to use to pull a changeset's metadata from 1 sfdc environment and validate to another sfdc environment running default tests

Lots of flexible once up and running (can change to deploy immediately, or to run specific tests only)

Please check SFDC Ant Migration Tool documentation for more info: https://developer.salesforce.com/docs/atlas.en-us.daas.meta/daas/forcemigrationtool_deploy.htm

# SETUP: build.properties file holds all environment variables
sf.usernameProduction = username for target org to validate against  
sf.usernameStaging = username for source org to pull metadata from changeset  
sf.passwordStaging = password for source org user  
sf.passwordProduction = password for target org user

sf.serverurl = https://login.salesforce.com - for prod orgs  
sf.testserverurl = https://test.salesforce.com - for sandbox orgs  
sf.releaseNumber = This is the exact name of change set in source org  
- try using a naming convention such as Release 1.1.1 or 1.1.1 for ease of use

# Running or Running single build steps
run via "ant -lib lib" to use the jars in the library folder and run all 3 build steps   
you can also run the targets individually such as "ant -lib lib retrieveChangeSet"  
this is helpful if you are blocked by dependencies but don't want to remove metadata from the change set  
- you can delete/edit metadata locally in the changeSet folder and then run "ant -lib lib deployEmptyCheckOnly" when ready

# build.xml steps
1. Deletes changeSet folder and recreates empty so we start with clean metadata "ant -lib lib cleanBuild"   
2. Retrieves metadata from change set by name from source org "ant -lib lib retrieveChangeSet"  
3. Validates against target org "ant -lib lib deployEmptyCheckOnly"