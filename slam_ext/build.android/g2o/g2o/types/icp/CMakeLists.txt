ADD_LIBRARY(types_icp ${G2O_LIB_TYPE}
  types_icp.cpp  types_icp.h
  g2o_types_icp_api.h
)

SET_TARGET_PROPERTIES(types_icp PROPERTIES OUTPUT_NAME ${LIB_PREFIX}types_icp)

TARGET_LINK_LIBRARIES(types_icp types_sba types_slam3d)
if(DEFINED ENV{BUILD_ANDROID_PROFILER_LIB})
message(STATUS "Profiler set: " $ENV{BUILD_ANDROID_PROFILER_LIB})
target_link_libraries(types_icp $ENV{BUILD_ANDROID_PROFILER_LIB})
add_definitions(-pg)
endif()
INSTALL(TARGETS types_icp
  RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
  LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
  ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
)

FILE(GLOB headers "${CMAKE_CURRENT_SOURCE_DIR}/*.h" "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp")

INSTALL(FILES ${headers} DESTINATION ${CMAKE_INSTALL_PREFIX}/include/g2o/types/icp)
