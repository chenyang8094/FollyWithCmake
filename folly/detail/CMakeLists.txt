#
# Copyright (C) 2017, yumo
#

set(FOLLY_DETAIL_SRCS
    CacheLocality.cpp
	Futex.cpp
	IPAddress.cpp
	MallocImpl.cpp
	MemoryIdler.cpp
	RangeCommon.cpp
	RangeSse42.cpp
	SocketFastOpen.cpp
	StaticSingletonManager.cpp
	ThreadLocalDetail.cpp
)
add_library(folly_detail OBJECT ${FOLLY_DETAIL_SRCS})
