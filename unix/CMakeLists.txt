file(GLOB_RECURSE HEADERS FOLLOW_SYMLINKS LIST_DIRECTORIES false CONFIGURE_DEPENDS *.h)
file(GLOB_RECURSE SOURCES FOLLOW_SYMLINKS LIST_DIRECTORIES false CONFIGURE_DEPENDS *.c *.cpp)

add_library(7z STATIC ${HEADERS} ${SOURCES})

target_compile_definitions(7z PRIVATE
    UNICODE
    _UNICODE
    _NO_CRYPTO
    _FILE_OFFSET_BITS=64
    _LARGEFILE_SOURCE
    _REENTRANT
    ENV_UNIX
)
if(MACOS)
    target_compile_definitions(7z PRIVATE ENV_MACOSX)
endif()
target_include_directories(7z PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/C>"
)
target_include_directories(7z PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/CPP>"
)
target_include_directories(7z PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/CPP/myWindows>"
)
target_include_directories(7z PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/CPP/include_windows>"
)
