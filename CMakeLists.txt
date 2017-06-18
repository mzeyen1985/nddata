# header-only CMakeLists.txt template

# minimum cmake version requirement
cmake_minimum_required(VERSION 3.5.1)

# project name
project(ndd)

# capital project name string
string(TOUPPER ${PROJECT_NAME} NAME_ID)

# option for installing the target
option(${NAME_ID}_INSTALL
	"Install the include headers of ${PROJECT_NAME}."
	ON
)

# add interface header files
set(PROJECT_INTERFACE_HEADER_FILES
	include/ndd/ndarray.hpp
	include/ndd/detail/ndarray.inl
	include/ndd/nddata.hpp
	include/ndd/detail/nddata.inl
	include/ndd/ndrecord.hpp
	include/ndd/detail/ndrecord.inl
	include/ndd/ndtype.hpp
	include/ndd/detail/ndtype.inl
)

# add header-only target
add_library(${PROJECT_NAME} INTERFACE)

# add compile flags
# if no flags need to be set, this command needs to be commented out
#target_compile_options(${PROJECT_NAME}
#	INTERFACE ${CXX_COMPILE_FLAGS}
#)

# add include directories
target_include_directories(${PROJECT_NAME}
	INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# add library dependencies
target_link_libraries(${PROJECT_NAME}
)

# install instructions
if(${NAME_ID}_INSTALL)
	install(FILES
		${PROJECT_INTERFACE_HEADER_FILES}
		DESTINATION include/${PROJECT_NAME}
	)
endif()