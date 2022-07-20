# SK-Fixed
Spiral Knights patched with bugfixes and tweaks.

NOTE: Only steam (Win x64) + standalone (Win x64) have been verified.
Please open an issue for other platforms, except steam (linux x64).
Known issue on Grey Haven's part with only 32 bit linux support for a JNI library.

To patch Java:
1. Download the zip from https://jdk.java.net/19/
2. Extract the jdk-19 folder
3. Delete your old java_vm folder and replace it with jdk-19 renamed as java_vm.
4. Most of the files inside Modified Files are there to fix compatibility with latest java,
so they are all necessary, except for projectx-pcode.jar.

Changes for SK, if you use the provided projectx-pcode.jar file:
- No AFK kick
- Low latency netcode patch.
	- Upgrades from 10 tick to 14 tick.
	- Fixes an input drop bug experienced with high fps.
	- Disables movement interpolation of entities on screen, to reduce buffering.

# For GH trying to fix Java 19 compatibility:

1. Remove "jvmarg = -XX:+AggressiveOpts" from getdown.txt. It is an invalid unrecognized argument in more recent versions.
See https://bugs.openjdk.org/browse/JDK-8150552
2. Update LWJGL dlls to the latest 2.9.3 version. The currently shipped native libs are incompatible with Java 9+.
3. Remove references to the .JNIFILE version of an lwjgl native lib for the OSX build, and replace with references only to the .dylib version.
See https://github.com/LWJGL/lwjgl/issues/100
4. Specify "--add-opens=java.*****=ALL-UNNAMED" type arguments for every single internal JDK API used.
In Java 16+, due to JEP 261 (https://openjdk.org/jeps/261), strong encapsulation is enabled by default,
and assumed internal JDK APIs are illegal to be utilized via reflection. You can manually break this still 
via "--add-opens" or "--add-exports" commands.