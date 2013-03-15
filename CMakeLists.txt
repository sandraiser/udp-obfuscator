cmake_minimum_required(VERSION 2.8)
project(udp_obfuscator CXX)

set(BOOST_ROOT "")

find_package(Boost REQUIRED system)
include_directories(${Boost_INCLUDE_DIRS})

add_executable(udp_obfuscator src/udp_forward.cpp src/udp_obfuscator.cpp)
target_link_libraries(udp_obfuscator ${Boost_LIBRARIES})
if (UNIX)
   target_link_libraries(udp_obfuscator pthread)
   set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
   set(MY_LINK_FLAGS "-std=c++11")
   if (APPLE)
      set(CMAKE_CXX_FLAGS "-stdlib=libc++ ${CMAKE_CXX_FLAGS}")
      set(MY_LINK_FLAGS "-stdlib=libc++ ${MY_LINK_FLAGS}")
   endif ()
   set_target_properties(udp_obfuscator PROPERTIES LINK_FLAGS ${MY_LINK_FLAGS})
endif ()