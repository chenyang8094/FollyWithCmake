#
# Copyright (C) 2017, yumo
#

set(FOLLY_BUILD_SRCS
	FormatTables.cpp
	GenerateFingerprintTables.cpp
)
add_library(folly_build OBJECT ${FOLLY_BUILD_SRCS})
