#
# Copyright (C) 2017, yumo
#

set(FOLLY_EXPERIMENTAL_IO_SRCS
	#AsyncIO.cpp
	FsUtil.cpp
	HugePages.cpp
	HugePageUtil.cpp
)
add_library(folly_experimental_io OBJECT ${FOLLY_EXPERIMENTAL_IO_SRCS})

