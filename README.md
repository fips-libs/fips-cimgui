# fips-cimgui

fipsified cimgui lib (https://github.com/cimgui/cimgui)

fips build system: https://github.com/floooh/fips

## How to integrate:

Add the dependency to your fips.yml file:

```yaml
imports:
    fips-cimgui:
        git: https://github.com/fips-libs/fips-cimgui
```

Use cimgui as dependency in your targets:

```cmake
fips_begin_*(...)
    ...
    fips_deps(cimgui)
fips_end_*(...)
```

Do not link both with ImGui and cimgui to the same target, cimgui comes
with its own Dear ImGui, and this would clash with another Dear ImGui
linked to the same project.

Include the cimgui header like this:

```c
#define CIMGUI_DEFINE_ENUMS_AND_STRUCTS
#include "cimgui/cimgui.h"
```

