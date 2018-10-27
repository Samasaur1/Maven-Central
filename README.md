# Adding a New Dependency to this repo.

1. Create a new branch for the dependency you are adding. **Do not** directly add new dependencies to `master`.
2. On the new branch, run the following command, substituting in the correct values for the different parameters:
    ```bash
    mvn install:install-file -DgroupId=$YOUR_GROUP -DartifactId=$YOUR_ARTIFACT -Dversion=$YOUR_VERSION -Dfile=$YOUR_JAR_FILE -Dpackaging=jar -DgeneratePom=true -DlocalRepositoryPath=. -DcreateChecksum=true
    ```

    * An example of this command for the TalonSRX Java library is shown below:

    ```bash
    mvn install:install-file -DgroupId=com.ctr-electronics -DartifactId=TalonSRXLibJava -Dversion=4.4.1.8 -Dfile=TalonSRXLibJava.jar -Dpackaging=jar -DgeneratePom=true -DlocalRepositoryPath=. -DcreateChecksum=true
    ```
   * **NOTE**: The file path to the JAR does not support expanding `~` as a user's home directory. File paths must be relative to the current directory or absolute, *without* using `~`.
3. Confirm that the installation was successful (twice).
4. If you're confident that installation was successful, merge with master and push.

# Using the Dependency in Gradle

1. In your Gradle build file, add the Maven repository `https://raw.githubusercontent.com/Samasaur1/Maven-Central/master` as shown below:

    ```groovy
    repositories {
        mavenCentral()
        maven { url 'https://raw.githubusercontent.com/Samasaur1/Maven-Central/master' }
        ...
    }
    ```

2. In your Gradle dependencies, add the following line, substituting in the correct values (which you entered in earlier when installing the dependency):

    ```groovy
    dependencies {
        compile group: '{GROUP-ID}', name: '{ARTIFACT-NAME}', version: '{VERSION}'
    }
    ```

3. Build and cross your fingers…
