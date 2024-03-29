#
# project: fips-cimgui
#
if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 3.0)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup(PROJECT fips-cimgui)
endif()

fips_begin_lib(cimgui)
    fips_dir(cimgui)
    fips_files(cimgui.cpp cimgui.h)
    fips_dir(cimgui/imgui)
    fips_files(
        imgui.h 
        imgui.cpp 
        imconfig.h
        imgui_demo.cpp
        imgui_draw.cpp 
        imgui_internal.h
        imgui_tables.cpp
        imgui_widgets.cpp
        imstb_rectpack.h 
        imstb_textedit.h 
        imstb_truetype.h 
    )
fips_end_lib()
target_include_directories(cimgui PUBLIC .)

if (FIPS_CLANG)
    # temp workaround for https://github.com/cimgui/cimgui/issues/166
    target_compile_options(cimgui PUBLIC -Wno-unused-parameter -Wno-typedef-redefinition)
endif()

if (FIPS_CLANG OR FIPS_GCC)
    target_compile_options(cimgui PUBLIC -Wno-return-type-c-linkage)
elseif (FIPS_MSVC)
    target_compile_options(cimgui PUBLIC /wd4190)
endif()

if (NOT FIPS_IMPORT)
    fips_finish()
endif()


