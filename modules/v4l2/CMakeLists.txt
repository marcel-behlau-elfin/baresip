project(v4l2)

if(WIN32)
  return()
endif()

find_package(V4L2)

if(NOT V4L2_FOUND)
  return()
endif()

list(APPEND MODULES_DETECTED ${PROJECT_NAME})
set(MODULES_DETECTED ${MODULES_DETECTED} PARENT_SCOPE)

set(SRCS v4l2.c)

if(STATIC)
  add_library(${PROJECT_NAME} OBJECT ${SRCS})
else()
  add_library(${PROJECT_NAME} MODULE ${SRCS})
endif()

target_include_directories(${PROJECT_NAME} PRIVATE ${V4L2_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PRIVATE ${V4L2_LIBRARIES})
