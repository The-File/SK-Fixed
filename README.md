# Spiral Knights patchset for Java 23

NOTE: Only steam (Win x64) + standalone (Win x64) have been verified.
Other platforms have been removed for now due to lackof testing and/or known issues on GH's part.

## If the game does not boot on fresh windows 10/11 installs:

### Specifically if you haven't tried these patches yet, and SK does not work out of the box at all with its default Java.

### Install Java 6 from https://archive.org/details/jdk-6u45-windows-x64 before trying the Java 23 patchset.

## Steps for users to follow:

To patch Java:
1. Download the zip from https://jdk.java.net/23/
2. Extract the jdk-23 folder
3. Delete your old java_vm folder and replace it with jdk-23 renamed as java_vm.
4. Select the folder for your OS, and overwrite in the according SK installation folder.

Note: Stable Java 22 works as well, via https://jdk.java.net/22/.

# For GH trying to fix Java 23 compatibility (Users ignore, meant for GH devs):

1. Remove "jvmarg = -XX:+AggressiveOpts" from getdown.txt. It is an invalid unrecognized argument in more recent versions.
See https://bugs.openjdk.org/browse/JDK-8150552
2. Update the supporting OpenAL and JInput JNI files (.dll, .so, .dylib) to the latest versions found bundled with LWJGL 2.9.3. Additionally, the file jinput.jar under the code directory as well needs replacement.
3. Remove references to the .JNIFILE version of an lwjgl native lib for the OSX build, and replace with references only to the .dylib version.
See https://github.com/LWJGL/lwjgl/issues/100
4. Specify "--add-opens=java.*****=ALL-UNNAMED" type arguments for every single internal JDK API used.
In Java 16+, due to JEP 261 (https://openjdk.org/jeps/261), strong encapsulation is enabled by default,
and assumed internal JDK APIs are illegal to be utilized via reflection. You can manually break this still 
via "--add-opens" or "--add-exports" commands.
5. For linux, recompile libfroth to be 64 bit, and distribute updated steam_api libs.
