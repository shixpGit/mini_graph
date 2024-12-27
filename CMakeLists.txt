cmake_minimum_required(VERSION 3.15.2)

project(mini_graph
	VERSION 0.1.0
	DESCRIPTION "A simple graph imp")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# export database to compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB_RECURSE SOURCES src/*.cpp)
add_library(mini_graph STATIC ${SOURCES})
target_include_directories(mini_graph PUBLIC include)
install(TARGETS mini_graph DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)
if(ANDROID)
  target_link_libraries(mini_graph PUBLIC log)
elseif(OHOS)
  target_link_libraries(mini_graph PUBLIC hilog_ndk.z)
endif()

if (TARGET gtest)
  message(STATUS "gtest is already defined")
else()
  set(GOOGLETEST_VERSION 1.15.2)
  add_subdirectory(${PROJECT_SOURCE_DIR}/third_party/googletest/googletest)
  #enable_testing()
  add_subdirectory(test)
endif()
