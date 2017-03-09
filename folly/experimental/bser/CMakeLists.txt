#
# Copyright (C) 2017, yumo
#

set(FOLLY_EXPERIMENTAL_BSER_SRCS
	Dump.cpp
	Load.cpp
)
add_library(folly_experimental_bser OBJECT ${FOLLY_EXPERIMENTAL_BSER_SRCS})

