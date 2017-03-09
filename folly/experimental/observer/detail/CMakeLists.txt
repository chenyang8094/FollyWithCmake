#
# Copyright (C) 2017, yumo
#

set(FOLLY_EXPERIMENTAL_DETAIL_SRCS
	Core.cpp
	ObserverManager.cpp
)
add_library(folly_experimental_detail OBJECT ${FOLLY_EXPERIMENTAL_DETAIL_SRCS})

