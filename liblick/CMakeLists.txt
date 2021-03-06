set(lib_name "lick")
set(lib_static_name "lick_static")

configure_file(
    "${PROJECT_SOURCE_DIR}/liblick/config.h.in"
    "${PROJECT_BINARY_DIR}/liblick/config.h")


set(sources
    "boot-loader.c"
    "boot-loader/9x.c"
    "boot-loader/me.c"
    "boot-loader/nt.c"
    "boot-loader/uefi.c"
    "boot-loader/boot-loader-utils.c"
    "boot-loader/vista.c"
    "distro.c"
    "distro/fatdog.c"
    "distro/puppy.c"
    "distro/distro-utils.c"
    "drives.c"
    "install.c"
    "lickdir.c"
    "llist.c"
    "llist-type.c"
    "menu.c"
    "menu/grub2.c"
    "menu/grub4dos.c"
    "menu/edit-flat-menu.c"
    "menu/menu-utils.c"
    "scandir.c"
    "system-info.c"
    "uniso.c"
    "utils/file-utils.c"
    "utils/fs-utils.c"
    "utils/id-utils.c"
    "utils/string-utils.c"
    "utils/system-utils.c")

set(inc_dirs
    ${inc_dirs}
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}/libarchive/include
    ${PROJECT_BINARY_DIR}/liblick)

set(link_dirs
    ${link_dirs}
    ${CMAKE_BINARY_DIR}/libarchive/lib)

set(libs
    ${libs}
    archive)

include_directories(${inc_dirs})
link_directories(${link_dirs})
add_library(${lib_name} SHARED ${sources})
add_library(${lib_static_name} STATIC ${sources})
target_link_libraries(${lib_name} ${libs})
add_dependencies(${lib_name} ${external_projects})
add_dependencies(${lib_static_name} ${external_projects})
