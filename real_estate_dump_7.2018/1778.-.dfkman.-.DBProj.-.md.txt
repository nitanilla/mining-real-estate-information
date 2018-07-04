# Fupa Troopas Real Estate Company

This is a team project for CSCI 320 at the Rochester Institute of Technology.

Team Members:
- Mark Nash
- Kurt Gregorek

We are charged with creating a user interface written in Java to simulate a
real estate company with H2 SQL database integration.

## Platform

The DB Project uses JavaFX for graphical rendering and H2 for data tracking.

# Execution:
## COMPILATION
Run in a command line:
“javac -Xlint:unchecked -classpath "DB/h2-1.4.197.jar" -d <Preferred Directory>  -sourcepath "src" src/sample/Main.java”
Now, add the extra files for execution:
In the preferred directory, add the Res folder and the DB folder.

## RUNNING
In the preferred directory:
Run:
“java -classpath ".;./DB/h2-1.4.197.jar" sample.Main”
-if in *NIX use : instead of ;

IF Java throws an error about a broken connection, try connecting via h2 console first to MarkDB




