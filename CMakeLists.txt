cmake_minimum_required(VERSION 2.8)

project(maia)

set(MAIA_LIB_MAJOR_VERSION "0")
set(MAIA_LIB_MINOR_VERSION "2")
set(MAIA_LIB_PATCH_VERSION "0")

#---------------------------------------------------------------------------$
#                             QT
#---------------------------------------------------------------------------$
# Find Qt4
find_package(Qt4 4.8.1 COMPONENTS QtCore QtNetwork QtXml REQUIRED)

# Include the cmake file needed to use qt4
include(${QT_USE_FILE})

#------------------------------------------------------------------------------
#                             INCLUDE DIRECTORIES
#------------------------------------------------------------------------------

include_directories(
	${PROJECT_SOURCE_DIR}
)

SET(SOURCES
	maiaObject.cpp 
	maiaFault.cpp 
	maiaXmlRpcClient.cpp 
	maiaXmlRpcServer.cpp 
	maiaXmlRpcServerConnection.cpp
)

SET(HEADERS
	maiaObject.h 
	maiaFault.h 
	maiaXmlRpcClient.h 
	maiaXmlRpcServer.h 
	maiaXmlRpcServerConnection.h
)

SET(MOC_HEADERS
    maiaObject.h
    maiaFault.h
    maiaXmlRpcClient.h
    maiaXmlRpcServer.h
    maiaXmlRpcServerConnection.h
)

#------------------------------------------------------------------------------
#                                Qt MACROS
#------------------------------------------------------------------------------
qt4_wrap_cpp(MOC_OUTFILES ${MOC_HEADERS})

#------------------------------------------------------------------------------
#                                LIBRARY
#------------------------------------------------------------------------------
add_library(maia STATIC
	${SOURCES}
	${HEADERS}
	${MOC_OUTFILES}
)

set_target_properties(maia PROPERTIES
	VERSION ${MAIA_LIB_MAJOR_VERSION}.${MAIA_LIB_MINOR_VERSION}.${MAIA_LIB_PATCH_VERSION}
	SOVERSION ${MAIA_LIB_MAJOR_VERSION}
)

target_link_libraries(maia
	${QT_LIBRARIES}
)

INSTALL( TARGETS maia 
	RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
	LIBRARY DESTINATION ${LIB_INSTALL_DIR}
    ARCHIVE DESTINATION ${LIB_INSTALL_DIR}
)
