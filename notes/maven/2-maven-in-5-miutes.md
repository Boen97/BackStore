## installation
1. tar xzvf apache-maven-3.8.5-bin.tar.gz
2. export PATH=/opt/apache-maven-3.8.5/bin:$PATH
3. `mvn -v`

## create a project
```
mvn 
archetype:generate 
-DgroupId=com.mycompany.app 
-DartifactId=my-app 
-DarchetypeArtifactId=maven-archetype-quickstart 
-DarchetypeVersion=1.4 
-DinteractiveMode=false
```
- executed the **Maven goal archetype:generate**
- and passed in various parameters to that goal
- the prefix **archetype** is the **plugin** that provies the **goal**
- the **archetype:generate goal** created a simple project based upon a **maven-archetype-quickstart** archetype
- a **plugin** is a collection of goals with a general common purpose

### standard project structure
my-app
    pom.xml
    src
        main
            java
                com
                    rhyme
                        app
                            App.java
        test
            java
                com
                    rhyme
                        app
                            AppTest.java
                        
### build the project

> `mvn package`
- rather than a goal, this is a **phase**
- a **phase** is a step in the **build lifecycle**, which is an ordered sequence of phases
  : validate
  : compile
  : test
  : package
  : verify
  : install
  : deploy
- when a phase is given, Maven executes every phase in the sequence up to and including the one defined.

> test the newly compiled and packaged JAR with the following command.
- `java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App`
- -cp class search path of directories and zip/jar files

### running Maven Tools

#### Maven Phases
1. validate
   : validate the project is correct and all necessary information is available

2. compile
   : compile the source code of the project

3. test
   : test the compiled source code using a suitable unit testing framework
   : these tests should not require the code be packaged or deployed

4. package
   : take the compiled code and package it in its distributable format, such as a JAR

5. integration-test
   : process and deploy the package if necessary into a environment where integration tests can be run.

6. verify
   : run any checkes to verify the package is valid and meets quality criteria

7. install
   : install the package into the local repository, for use as a dependency in other projects locally

8. depoly:
   : done in an integration or release environment
   : copies the final package to the remote repository for share with other developers 
   : and projects

9. clean
   : cleans up artifacts created by prior builds

10. site
    : generates site documentation for this project

> Phases are actually mapped to underlying goals.

> `mvn clean dependency:copy-dependencies package`
: phases and goals may be executed in sequence

#### generating the site
- `mvn site`
: This phase generates a site based upon information on the project's pom
: You can look at the documentation generated under target/site.
