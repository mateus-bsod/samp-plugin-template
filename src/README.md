
# Global Variables
```c
void** ppPluginData;
extern void* pAMXFunctions;
```

- ``ppPluginData`` Pointer array passed by the SA-MP server containing exported interfaces and utilities.</br>
- ``pAMXFunctions`` Required by the AMX API to access internal Pawn VM functions. Must be initialized during plugin loading.</br>

# Plugin Capability Declaration
```c
PLUGIN_EXPORT unsigned int PLUGIN_CALL Supports()
{
	return SUPPORTS_VERSION | SUPPORTS_AMX_NATIVES;
}
```
This function informs the SA-MP server which features the plugin supports.

### Flags:

- ``SUPPORTS_VERSION`` Indicates compatibility with the current SA-MP version.</br>
- ``SUPPORTS_AMX_NATIVES`` Enables registration of custom Pawn natives.</br>

# Plugin Load Callback
```c
PLUGIN_EXPORT bool PLUGIN_CALL Load(void** ppData)
{
	pAMXFunctions = ppData[PLUGIN_DATA_AMX_EXPORTS];
	logprintf = (logprintf_t)ppData[PLUGIN_DATA_LOGPRINTF];

	logprintf("=> HelloWorld plugin load.");
	return true;
}
```
Executed when the plugin is loaded by the SA-MP server.

### Responsibilities:
- Store the AMX function table (``PLUGIN_DATA_AMX_EXPORTS``)</br>
- Retrieve the ``logprintf`` function pointer</br>
- Perform initialization logic</br>
- Return true to signal successful loading</br>

---

# Native Implementation
```c
cell AMX_NATIVE_CALL HelloWorld(AMX* amx, cell* params)
{
	logprintf("Hello World!");
	return 0;
}
```
Defines a Pawn native function.

### Parameters:

- ``AMX* amx`` Pointer to the Pawn virtual machine instance.</br>
- ``cell* params`` Array containing native arguments (if any).</br>

# Native Registration Table
```c
AMX_NATIVE_INFO PluginNatives[] =
{
	{ "HelloWorld", HelloWorld },
	{ 0, 0 }
};
```
Defines the mapping between Pawn native names and C/C++ function pointers. </br>
- The array must be null-terminated. </br>
- The string name is what Pawn scripts will call. </br>
