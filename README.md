# [NMRiH] VScript Proxy

Call No More Room in Hell's VScript functions from within Sourcemod

## Usage
- Drag and drop `vscript_proxy.inc` into spcomp's `include` directory
- `#include <vscript_proxy>` in your script

## Natives List
All natives are documented in the [.inc](https://github.com/dysphie/nmrih-vscript-proxy/blob/main/vscript_proxy.inc)

- RunEntVScript
- RunEntVScriptEnt
- RunEntVScriptBool
- RunEntVScriptFloat
- RunEntVScriptVector
- RunEntVScriptString


## Example script

```cpp
#include <sdktools>
#include <vscript_proxy>

public void OnPluginStart()
{
    RegConsoleCmd("test_proxy", test_proxy);
}

Action test_proxy(int client, int args)
{
    PrintToServer("GetOwner(): %d", RunEntVScriptEnt(client, "GetOwner()"));

    RunEntVScript(client, "ViewPunch(Vector(10, 0, 0))");

    PrintToServer("IsAlive(): %d", RunEntVScriptBool(client, "IsAlive()"));
    PrintToServer("GetJumpStaminaCost(): %f", RunEntVScriptFloat(client, "GetJumpStaminaCost()"));

    float vec[3];
    RunEntVScriptVector(client, "GetAngles()", vec);
    PrintToServer("GetAngles(): %f %f %f", vec[0], vec[1], vec[2]);

    char str[32];
    RunEntVScriptString(client, "GetClassname()", str, sizeof(str));
    PrintToServer("GetClassname(): %s", str);

    return Plugin_Handled;
}
```

## Special Thanks
- Silvers for the [original idea](https://forums.alliedmods.net/showthread.php?t=317145)
- [Felis](https://github.com/felis-catus) for adding `logic_script_proxy` to the game
