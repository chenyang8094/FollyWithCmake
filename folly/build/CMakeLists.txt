#
# Copyright (C) 2017, yumo
#

set(FOLLY_BUILD_SRCS
	EscapeTables.cpp
	FormatTables.cpp
	GenerateFingerprintTables.cpp
	GroupVarintTables.cpp
)
add_library(folly_build OBJECT ${FOLLY_BUILD_SRCS})
