include(lib/cmake/GitRevision.cmake)
git_rev_parse(YOSYS_SLANG_REVISION ${CMAKE_CURRENT_SOURCE_DIR}/lib)
git_rev_parse(SLANG_REVISION ${PROJECT_SOURCE_DIR}/libs/slang)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/lib/src/version.h.in ${CMAKE_CURRENT_BINARY_DIR}/version.h)

yosys_frontend(slang
	lib/src/abort_helpers.cc
	lib/src/addressing.cc
	lib/src/async_pattern.cc
	lib/src/async_pattern.h
	lib/src/blackboxes.cc
	lib/src/builder.cc
	lib/src/cases.cc
	lib/src/cases.h
	lib/src/diag.cc
	lib/src/diag.h
	lib/src/initialization.cc
	lib/src/lvalue.cc
	lib/src/memory.h
	lib/src/naming.cc
	lib/src/procedural.cc
	lib/src/slang_frontend.cc
	lib/src/slang_frontend.h
	lib/src/statements.h
	lib/src/sva.cc
	lib/src/variables.cc
	lib/src/variables.h
	${CMAKE_CURRENT_BINARY_DIR}/version.h
	INCLUDE_DIRS
		${CMAKE_CURRENT_BINARY_DIR}
	LIBRARIES
		slang::slang
		fmt::fmt
)

# TODO: remove next line when warnings/errors are fixed
set_target_properties(yosys_read_slang PROPERTIES YOSYS_IS_ABC ON)
