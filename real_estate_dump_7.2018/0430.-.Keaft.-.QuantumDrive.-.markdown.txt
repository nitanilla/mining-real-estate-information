# Readme #

This is the source distribution for the QuantumDrive project.

It is licensed under the GNU General Public License version 3.

## About ##

QuantumDrive is a game written for the JVM, primarily targeting
the [OpenPandora][] portable gaming platform. It is a real time
strategy game that tries to unite many of the features found in
other major RTS titles while also trying to simplify them and
make them usable using a touch screen and very limited screen
real estate. Our goal is to make the game extremely modular and
extensible, to make it possible for our users to adapt and adopt
our game to suit their needs.

To find out more about the project, check out the [wiki][]. Also
feel free to join the discussion over at our [forum][]; we
appreciate your participation there even if you don't plan to
contribute to the project.

## Building the source code ##

The latest version of the source code can always be found
at [GitHub][]. There, you'll also find our [wiki][] and all of
the information we've put in it for your convenience.

In order to build the code, you'll need three tools:

*   A [Java JDK][1].
*   The [Apache Maven][2] build system.
*   The [Git][3] source code management tool.

You can find out how to install these tools (and more) by 
reading our [forum guide][4].

When you have all three tools installed, use the following two
(or actually three) steps to compile the project for your
platform:

    git clone git://github.com/Keaft/QuantumDrive.git
    cd QuantumDrive
    mvn install -P profile

Instead of "profile", you have to specify one of our build
profiles. These are:

*   "linux-i586" - Linux for 32-bit Intel and AMD processors
*   "linux-amd64" - Linux for 64-bit Intel and AMD processors
*   "macosx-universal" - Any Apple Mac version, either with an
    Intel or PPC processor
*   "windows-i586" - Any 32-bit Windows version
*   "windows-amd64" - Any 64-bit Windows version
*   "solaris-i586" - OpenSolaris for 32-bit Intel and AMD
    processors
*   "solaris-sparc" - Sun Solaris for SPARC-processors
    (Yes, we support that!)
*   "solaris-sparcv9" - Sun Solaris for SPARCv9 processors

If no profile is specified, we will try to guess which operating
system you're currently running and build a distribution based
on that information. That is why you will find more build
configurations in the pom.xml than the ones that are listed above;
they are used for automatic detection.

We do not currently support using multiple profiles at once.

Since the OpenPandora isn't released yet, we cannot currently
deploy for it, either.

You will find various generated distributions of our project
(either as JARs with and without dependencies, or as complete
ZIP distributions) in the "target/" folder.

## Joining in ##

If you want to contribute to the project in any shape or form,
please visit us at our [forum][]. Make yourself known, tell us
what you can do, and we'll be sure to make use of your skills
somehow.

[github]:      http://github.com/Keaft/QuantumDrive      "QuantumDrive GitHub repository"
[forum]:       http://quantumdrive.dyndns.org/           "QuantumDrive Forum"
[wiki]:        http://wiki.github.com/Keaft/QuantumDrive "QuantumDrive Wiki"
[openpandora]: http://openpandora.org/                   "OpenPandora - The OMAP3 based Handheld"

[1]:           http://java.sun.com/javase/downloads/index.jsp
[2]:           http://maven.apache.org/
[3]:           http://git-scm.com/
[4]:           http://quantumdrive.dyndns.org/programming/development-resources-and-tools/