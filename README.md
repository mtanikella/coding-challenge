## Notes

It is optional to first (re)build the jar file from scratch (instructions below).<br/>
Or directly run w/ the already built jar file. See Running the application from the command line section below).

For encoding/decoding JSON objects, the gson library was used. See build.gradle for details.<br/>
See the Project Layout section regarding testing.

## Install Java

Install Java if not already installed. The current code was built and tested using Java 18 on macOS.

## Gradle

The build framework provided here uses gradle to build the project and manage the dependencies.  The `gradlew` command used here will
automatically download gradle so there is no need to install anything other than java.

### Project Layout

All source code is located in the `src/main/java` folder.
There is only one source file: JSONUtils.java, which contains the flatten method.
The testing files are located in the `src/test/java` folder.
Corresponding to the source file, there is one JUnit test file: JSONUtilsTest.java.
The file contains two tests: testValidJson, and testInvalidJson.
testValidJson is a parametrized test.
It takes a list of inputs and expected flattened outputs, and asserts that the actual flattened output equals the expected output.

### Building the project from the command line

To build the project on Linux or MacOS run the command `./gradlew build` 
in a shell terminal.  This will build the source code in
`src/main/java`, run any tests in `src/test/java` and create two output
jar files in the `build/libs` folder: `mongodb-coding-challenge-shadow.jar` and `mongodb-coding-challenge.jar`.

To clean out any intermediate files run `./gradlew clean`.  This will remove all files in the `build` folder.

### Running the application from the command line

Start the application by running the command
`java -jar ./build/libs/mongodb-coding-challenge-shadow.jar`

The input is expected via stdin, so after typing the above command, hit Return.
Then input a valid JSON object string, and hit Return.
The output is sent to std.out.

##### Valid runs
`java -jar ./build/libs/mongodb-coding-challenge-shadow.jar 
{"a": 1, "b": true, "c": {"d": 3,"e": "test"}}
{"a":1,"b":true,"c.d":3,"c.e":"test"}

test.json contains same input as above<br/>
`cat test.json | java -jar ./build/libs/mongodb-coding-challenge-shadow.jar`<br/>
{"a":1,"b":true,"c.d":3,"c.e":"test"}

##### Invalid run
Note the missing brace at the end of the input<br/>
`java -jar ./build/libs/mongodb-coding-challenge-shadow.jar`<br/>
{"a": 3<br/>
Input is not a valid JSON object<br/>
