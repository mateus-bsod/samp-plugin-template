<div align="center">

# samp-plugin-template

[![Discord](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/PNCn2dMv3D)
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white) 
![License](https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge)

**samp plugin template for VS (.sln).**

</div>

### template.inc
This file is responsible for telling the server which functions were added using the include.

---


## 1. define
![define](https://github.com/mateus-bsod/samp-plugin-template/blob/main/imgs/define.png)
```C
#if defined _𝙔𝙊𝙐𝙍𝙄𝙉𝘾𝙇𝙐𝘿𝙀_included
    #endinput
#endif
#define _𝙔𝙊𝙐𝙍𝙄𝙉𝘾𝙇𝙐𝘿𝙀_included
```

Well, this is just a definition, that is, as the name itself says, it's a DEFINITION. It doesn't add or subtract anything important from your code.
However, its use may be useful in the future, since by clarifying to the compiler that your include is included, it's possible to know if it's present in the code or not.

Example:
```pawn
#if !defined _TEMPLATE_PLUGIN_included
    #error To use "native HelloWorld()" you need to use "template.inc"
#endif
```

There are several ways to declare this; there is no standard. Let's use some examples of includes:
#### a_samp.inc
```pawn
#if defined _samp_included
	#endinput
#endif
#define _samp_included
```

#### PawnPlus.inc
```pawn
#if defined _inc_PawnPlus
#undef _inc_PawnPlus
#endif

#if defined _PawnPlus_included
#endinput
#endif
#define _PawnPlus_included
```

## 2. native
Native functions are provided by the SA-MP server itself or by external plugins. Native functions are provided by the SA-MP server itself or by external plugins. In other words: if you create a function for a plugin, you need to explain to the server that you wrote it and that the function exists... and you explain this to the server using:

### [main.inc](https://github.com/mateus-bsod/samp-plugin-template/blob/main/src/main.cpp#L33)
![natives](https://github.com/mateus-bsod/samp-plugin-template/blob/main/imgs/native.png)

⚠️ [Documentation for the "main.cpp" and "main.h" files](https://github.com/mateus-bsod/samp-plugin-template/blob/main/src/README.md)

### [template.inc](https://github.com/mateus-bsod/samp-plugin-template/blob/main/template.inc)
```pawn
native HelloWorld();
```
