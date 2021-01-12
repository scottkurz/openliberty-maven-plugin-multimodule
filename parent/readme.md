# this project is a demo of issue [https://github.com/OpenLiberty/ci.maven/issues/1078](https://github.com/OpenLiberty/ci.maven/issues/1078)

This project will show a web  module with a parent project, containing the openliberty maven plugin as a profile.

As a child of parent, a web module also contain a profile with same name as parent, but with some additional execution

The point of this is to be able to have one parent to rule the maven plugin into all downstreams web projects.

The parent is holding the most important plugin configs, but if the web module need some additional executions, it will add it. Else it will inherit all from parent.

My company has over 100 web modules, so to adminster 100 copies of the plugin config, would be a nigthmare


## Steps to reproduce

```
1. check out the parent project
2. run mvn install in the parent project to get your parent installed into the local maven repo
3. goto web module, execute mvn -Pliberty This will install it all, but will ignore the execution from parent and only execute 'web-child-module-frontend-additional-dependencies'
   look for the message :
   [WARNING] liberty-maven-plugin:deploy goal has multiple execution configurations (default to "web-child-module-frontend-additional-dependencies" execution)
4. inspect the lib folder in defaultserver, the ojdbc6.jar is missing
5. execute 'mvn install liberty:dev -Pliberty' and now both executions is running and the lib folder containg two jars.
   You will se two executions now:
   [INFO] --- liberty-maven-plugin:3.3.3:deploy (web-child-module-frontend-additional-dependencies) @ web-module ---
   ..
   ..
   [INFO] --- liberty-maven-plugin:3.3.3:deploy (deploy-additional-dependencies) @ web-module ---
   
     
```


