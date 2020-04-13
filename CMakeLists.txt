cmake_minimum_required(VERSION 3.1)

project(rapidxml VERSION 1.13.0 LANGUAGES CXX)

## CONFIGURATION
##
set(RAPIDXML_TARGET_NAME               ${PROJECT_NAME})
set(RAPIDXML_INCLUDE_BUILD_DIR "${PROJECT_SOURCE_DIR}/include")

##
## TARGET
##
message("Target name: ${RAPIDXML_TARGET_NAME}")
add_library(${RAPIDXML_TARGET_NAME} INTERFACE)
add_library(${PROJECT_NAME}::${RAPIDXML_TARGET_NAME} ALIAS ${RAPIDXML_TARGET_NAME})
target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_17)
target_include_directories(
    ${RAPIDXML_TARGET_NAME}
    INTERFACE $<BUILD_INTERFACE:${${PROJECT_NAME}_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)


##
## INSTALL
##
install(TARGETS ${PROJECT_NAME}
        EXPORT ${PROJECT_NAME}_Targets
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

include(CMakePackageConfigHelpers)
write_basic_package_version_file("${PROJECT_NAME}ConfigVersion.cmake"
                                 VERSION ${PROJECT_VERSION}
                                 COMPATIBILITY SameMajorVersion)

install(DIRECTORY include DESTINATION .)
