# SK-Fixed
Spiral Knights patched with bugfixes and tweaks.

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