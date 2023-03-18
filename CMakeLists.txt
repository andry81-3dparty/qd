cmake_minimum_required(VERSION 3.0)

include(tacklelib/Project)

project("qd")

set(PROJECT_LIB_NAME qd)

tkl_check_var(REQUIRED PATH   QD_BRANCH_NAME) # ex: `2_3_22_20181030`

set(PROJECT_EXTERNALS_DIR "_externals")
set(QD_EXTERNAL_SOURCE_DIR "${CMAKE_CURRENT_LIST_DIR}/${PROJECT_EXTERNALS_DIR}/${QD_BRANCH_NAME}")


tkl_check_var(OPTIONAL PATH QD_ROOT)
tkl_check_var(OPTIONAL . ENABLE_QD_INTEGRATION)
tkl_check_var(OPTIONAL . ENABLE_QD_QD_INTEGRATION)
tkl_check_var(OPTIONAL . ENABLE_QD_DD_INTEGRATION)


file(GLOB_RECURSE all_headers ${QD_EXTERNAL_SOURCE_DIR}/include/*.h*)
file(GLOB_RECURSE all_sources ${QD_EXTERNAL_SOURCE_DIR}/src/*.c*)

add_library(${PROJECT_LIB_NAME} STATIC ${all_headers};${all_sources})

tkl_initialize_library_target_defaults(${PROJECT_LIB_NAME} "anybit")

tkl_source_groups_from_dir_list("Header Files" FILES ${QD_EXTERNAL_SOURCE_DIR}/include *.h*)
tkl_source_groups_from_dir_list("Source Files" FILES ${QD_EXTERNAL_SOURCE_DIR}/src *.c*)

target_include_directories(${PROJECT_LIB_NAME}
  PUBLIC
    ${QD_EXTERNAL_SOURCE_DIR}/include
    ${QD_EXTERNAL_SOURCE_DIR}
)

if (DEFINED ENABLE_QD_INTEGRATION)
  tkl_add_target_compile_definitions(${PROJECT_LIB_NAME} *
    PUBLIC
      ENABLE_QD_INTEGRATION=${ENABLE_QD_INTEGRATION}
  )
endif()
if (DEFINED ENABLE_QD_QD_INTEGRATION)
  tkl_add_target_compile_definitions(${PROJECT_LIB_NAME} *
    PUBLIC
      ENABLE_QD_QD_INTEGRATION=${ENABLE_QD_QD_INTEGRATION}
  )
endif()
if (DEFINED ENABLE_QD_DD_INTEGRATION)
  tkl_add_target_compile_definitions(${PROJECT_LIB_NAME} *
    PUBLIC
      ENABLE_QD_DD_INTEGRATION=${ENABLE_QD_DD_INTEGRATION}
  )
endif()
