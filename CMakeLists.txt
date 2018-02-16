cmake_minimum_required(VERSION 3.9)
project(zhe C)

set(CMAKE_C_STANDARD 11)

add_compile_options(
  $<$<C_COMPILER_ID:MSVC>:/W3>
  $<$<C_COMPILER_ID:Clang>:-Wall>
  $<$<C_COMPILER_ID:AppleClang>:-Wall>
  $<$<C_COMPILER_ID:GNU>:-Wall>)

include_directories(
        "${PROJECT_SOURCE_DIR}/src"
        "${PROJECT_SOURCE_DIR}/example/platform"
        "${PROJECT_SOURCE_DIR}/example/configs/p2p"
)

file(GLOB Sources "src/*.c" "example/platform/*.c")
add_library(zhe ${Sources})

add_executable(throughput example/throughput/throughput.c)
target_link_libraries(throughput zhe)

add_executable(roundtrip example/roundtrip/roundtrip.c)
target_link_libraries(roundtrip zhe)

add_executable(spub example/simple/pub.c)
target_link_libraries(spub zhe)

add_executable(ssub example/simple/sub.c)
target_link_libraries(ssub zhe)

install (TARGETS zhe DESTINATION ${PROJECT_SOURCE_DIR}/lib)
install (TARGETS throughput DESTINATION ${PROJECT_SOURCE_DIR}/bin)
install (TARGETS roundtrip DESTINATION ${PROJECT_SOURCE_DIR}/bin)
install (TARGETS spub DESTINATION ${PROJECT_SOURCE_DIR}/bin)
install (TARGETS ssub DESTINATION ${PROJECT_SOURCE_DIR}/bin)