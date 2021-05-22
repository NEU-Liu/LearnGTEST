cmake_minimum_required(VERSION 3.10)
project(LearnGTEST)

set(CMAKE_CXX_STANDARD 14)

include_directories("fmt")
link_libraries("/home/liu/Desktop/LearnCC/fmt/Alib/libfmt.a")
FILE(GLOB fmt "fmt/Afmt")


#include_directories("Google/gmock")
#include_directories("Google/gtest")
#上面两条指令，将会导致REGISTER_TYPED_TEST_SUITE_P
#跳转到：/usr/local/include/gtest/gtest-typed-test.h
#而不是自定义目录的：Google/gtest/gtest-typed-test.h
#这样将会导致错误，因为我在link_libraris()时连接的静态文件是自定义的目录，
#主要原因是gtest版本等问题，导致了错误！
include_directories("Google")
#Notice the library order, the gmock is position gtest next!
link_libraries("/home/liu/Desktop/LearnCC/libs/libgtest.a")
link_libraries("/home/liu/Desktop/LearnCC/libs/libgtest_main.a")
link_libraries("/home/liu/Desktop/LearnCC/libs/libgmock.a")
link_libraries("/home/liu/Desktop/LearnCC/libs/libgmock_main.a")

link_libraries(pthread)


FILE(GLOB  Gmock  "Google/gmock")
FILE(GLOB  Gtest  "Google/gtest")



FILE(GLOB  example_cc  "example/*.cc")
FILE(GLOB  example_h  "example/*.h")

add_executable(LearnGTEST main.cpp   ${fmt} ${Gmock}  ${Gtest}   ${example_cc} ${example_h})
