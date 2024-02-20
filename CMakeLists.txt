# CMakeList.txt : Top-level CMake project file, do global configuration
# and include sub-projects here.
#
cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project("PracticeGameServer")

add_executable(PracticeGameServer "src/main.cpp")

if (MSVC)
    add_compile_options(/W4 /MP /external:anglebrackets /external:W0)
    if (CMAKE_BUILD_TYPE STREQUAL "Debug")
        add_compile_options(/WX /sdl)
    else()
        add_compile_options()
    endif()
endif()

include_directories("external/include/")
link_directories("external/lib/${CMAKE_BUILD_TYPE}/")

if (MSVC)
    link_libraries(enet.lib)
else()
endif()
