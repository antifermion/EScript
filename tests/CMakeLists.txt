# CMakeLists.txt
# This file is part of the EScript programming language (https://github.com/EScript)
#
# Copyright (C) 2011-2014 Claudius Jähn <ClaudiusJ@live.de>
# Copyright (C) 2011-2015 Benjamin Eikel <benjamin@eikel.org>
#
# Licensed under the MIT License. See LICENSE file for details.
# ---------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.1.0)

if(BUILD_ESCRIPT_TEST)
	add_executable(escript_test test.cpp)
	target_compile_definitions(escript_test PRIVATE ES_BUILD_TEST_APPLICATION)
	target_link_libraries(escript_test PRIVATE EScript)
	install(TARGETS escript_test
		RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} COMPONENT tests
		LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT tests
		ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} COMPONENT tests
	)
	# Install the EScript files needed for the tests
	install(
		DIRECTORY ./
		DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/EScript/tests
		COMPONENT tests
		FILES_MATCHING PATTERN "*.escript"
	)

	add_test(NAME TestEScript COMMAND escript_test WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/..)
endif()
