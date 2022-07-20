# Spiral Knights patchset for Java 19.

NOTE: Only steam (Win x64) + standalone (Win x64) have been verified.
Please open an issue for other platforms, except steam (linux x64).
Known issue on Grey Haven's part with only 32 bit linux support for a JNI library.

To patch Java:
1. Download the zip from https://jdk.java.net/19/
2. Extract the jdk-19 folder
3. Delete your old java_vm folder and replace it with jdk-19 renamed as java_vm.
4. Select the folder for your OS, and overwrite in the according SK installation folder.

# For GH trying to fix Java 19 compatibility:

1. Remove "jvmarg = -XX:+AggressiveOpts" from getdown.txt. It is an invalid unrecognized argument in more recent versions.
See https://bugs.openjdk.org/browse/JDK-8150552
2. Update the supporting OpenAL and JInput JNI files (.dll, .so, .dylib) to the latest versions found bundled with LWJGL 2.9.3. Additionally, the file jinput.jar under the code directory as well needs replacement.
3. Remove references to the .JNIFILE version of an lwjgl native lib for the OSX build, and replace with references only to the .dylib version.
See https://github.com/LWJGL/lwjgl/issues/100
4. Specify "--add-opens=java.*****=ALL-UNNAMED" type arguments for every single internal JDK API used.
In Java 16+, due to JEP 261 (https://openjdk.org/jeps/261), strong encapsulation is enabled by default,
and assumed internal JDK APIs are illegal to be utilized via reflection. You can manually break this still 
via "--add-opens" or "--add-exports" commands.