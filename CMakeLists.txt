cmake_minimum_required(VERSION 3.26)
project(cmake_share C)


set(CSRS "congshanruoshui")

message(STATUS "The content of CSRS is ${CSRS}")

unset(CSRS)

message(STATUS "The content of CSRS is ${CSRS}")


set(CSRS this is a good blogger)
message(STATUS "The content of CSRS is ${CSRS}")

set(CSRS "this;is;a;good;blogger")
message(STATUS "The content of CSRS is ${CSRS}")


list(APPEND CSRS "!")
message(STATUS "The content of CSRS is ${CSRS}")

list(FIND CSRS "blogger" BLOGGER_INDEX)
if(${BLOGGER_INDEX} LESS 0)
    message(STATUS "Not find \"blogger\" in CSRS")
else()
    message(STATUS "Find \"blogger\" in CSRS at index ${BLOGGER_INDEX}")
endif()

list(GET CSRS ${BLOGGER_INDEX} BLOGGER)
message(STATUS "The word in CSRS at index ${BLOGGER_INDEX} is ${BLOGGER}")


set(TEST_IF ON)
if(DEFINED TEST_IF)
    message(STATUS "TEST_IF is ON")
endif()

set(MONTH 12)
if(${MONTH} EQUAL 12)
    message(STATUS "MONTH is 12")
endif()

set(CSRS "CongShanRuoShui")
if(${CSRS} STREQUAL "CongShanRuoShui")
    message(STATUS "CSRS is CongShanRuoShui")
endif()

if((${MONTH} EQUAL 12) AND (${CSRS} STREQUAL "CongShanRuoShui"))
    message(STATUS "MONTH is 12")
    message(STATUS "CSRS is CongShanRuoShui")
endif()


set(test_while 5)
while(${test_while} GREATER 0)
    message(STATUS "test_while is ${test_while}")
    math(EXPR test_while "${test_while}-1")
endwhile()

set(test_foreach a b c d e)
foreach(item IN LISTS test_foreach)
    message(STATUS "item is ${item}")
endforeach()

foreach(item IN ITEMS a b c d e)
    message(STATUS "item is ${item}")
endforeach()

foreach(month RANGE 1 12)
    message(STATUS "month is ${month}")
endforeach()


function(test_function name year)
    message(STATUS "${name} is ${year} years old")
endfunction()

test_function(CSRS 18)

macro(test_macro name year)
    message(STATUS "${name} is ${year} years old")
endmacro()
test_macro(CSRS 18)



execute_process(
        # 要执行的命令
        COMMAND ls -al
        # 执行命令的目录
        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
        # 命令结果输出
        OUTPUT_VARIABLE result
        # 剔除输出尾部的空格
        OUTPUT_STRIP_TRAILING_WHITESPACE
        # 发送错误时停止执行
        ERROR_QUIET
)
message(STATUS "result is ${result}")


include(FindPkgConfig)
find_package(PkgConfig REQUIRED)

pkg_search_module(OPENSSL REQUIRED openssl)

if(OPENSSL_FOUND)
    message(STATUS "openssl is found")
endif()




set(CMAKE_C_STANDARD 11)

include_directories("utils")
add_library(utils SHARED
        utils/test_library.c
)
set_property(TARGET utils PROPERTY POSITION_INDEPENDENT_CODE ON)




add_executable(cmake_share main.c)
target_link_libraries(cmake_share utils)


#add_custom_command(
#        TARGET cmake_share
#        POST_BUILD
#        COMMAND mv cmake_share cmake_share_test
#)