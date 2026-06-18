add_subdirectory(bigint)
add_subdirectory(cxxopts)
add_subdirectory(dlfcn-win32)
add_subdirectory(ezsat)
add_subdirectory(fst)
add_subdirectory(json11)
add_subdirectory(minisat)
add_subdirectory(sha1)
add_subdirectory(subcircuit)
block()
    set(BUILD_SHARED_LIBS OFF)
    include(FetchContent)
    option(FMT_INSTALL OFF)
    FetchContent_Declare(
        fmt
        EXCLUDE_FROM_ALL
        SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/fmt
    )
    FetchContent_MakeAvailable(fmt)
    if (NOT YOSYS_WITHOUT_SLANG)
        set(SLANG_USE_MIMALLOC OFF)
        add_subdirectory(slang)
    endif()
endblock()
