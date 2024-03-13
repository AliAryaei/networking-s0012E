#--------------------------------------------------------------------------
# spacegame client
#--------------------------------------------------------------------------

PROJECT(client)
FILE(GLOB project_headers code/*.h)
FILE(GLOB project_sources code/*.cc)

SET(files_project ${project_headers} ${project_sources})
SET(files_proto)
flat_compile(proto.fbs)
SOURCE_GROUP("client" FILES ${files_project})

ADD_EXECUTABLE(client ${files_project} ${files_proto})
target_include_directories(client PRIVATE "${CMAKE_BINARY_DIR}/generated/flat")

TARGET_LINK_LIBRARIES(client core render)
ADD_DEPENDENCIES(client core render)

IF(MSVC)
    set_property(TARGET client PROPERTY VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
ENDIF()