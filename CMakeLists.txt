cmake_minimum_required(VERSION 3.0)
project(opcua-anmal-server)

set(UA_NAMESPACE_ZERO FULL CACHE STRING "" FORCE)
set(open62541_TOOLS_DIR "${CMAKE_SOURCE_DIR}/open62541/tools")
set(open62541_NODESET_DIR "${CMAKE_SOURCE_DIR}/open62541/deps/ua-nodeset")
add_subdirectory(open62541)

ua_generate_nodeset_and_datatypes(
        NAME "animal"
        FILE_CSV "${CMAKE_SOURCE_DIR}/opcua-animal-cs/Published/animal/animalModel.csv"
        FILE_BSD "${CMAKE_SOURCE_DIR}/opcua-animal-cs/Published/animal/animal.Types.bsd"
        NAMESPACE_IDX 2
        FILE_NS "${CMAKE_SOURCE_DIR}/opcua-animal-cs/Published/animal/animal.NodeSet2.xml"
        OUTPUT_DIR "${CMAKE_BINARY_DIR}/animal_cs"
        INTERNAL
)

include_directories(${CMAKE_BINARY_DIR}/animal_cs)

add_executable(server_animal
        src/server_animal.c
        ${UA_NODESET_ANIMAL_SOURCES}
        ${UA_TYPES_ANIMAL_SOURCES})
target_link_libraries(server_animal open62541::open62541)

add_dependencies(server_animal open62541-generator-ns-animal)