cmake_minimum_required(VERSION 3.9)

project(vterm C)

if(CMAKE_SYSTEM_NAME MATCHES Retro68)
add_compile_options(-mcpu=68020)
add_compile_options(-O3)
add_compile_options(-ffunction-sections)
endif()

if(CMAKE_SYSTEM_NAME MATCHES RetroPPC)
add_compile_options(-O3)
add_compile_options(-ffunction-sections)
endif()

add_compile_options(-Wno-attributes)

add_library(vterm STATIC src/encoding.c
                         src/keyboard.c
                         src/mouse.c
                         src/parser.c
                         src/pen.c
                         src/screen.c
                         src/state.c
                         src/unicode.c
                         src/vterm.c)

target_include_directories(vterm PUBLIC include)
target_include_directories(vterm PRIVATE src)

include(GNUInstallDirs)
install(FILES include/vterm.h include/vterm_keycodes.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(TARGETS vterm LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})


