#
# Copyright (C) 2017, yumo
#

set(FOLLY_FIBERS_DETAIL_SRCS
    AtomicBatchDispatcher.cpp
)
add_library(folly_fibers_detail OBJECT ${FOLLY_FIBERS_DETAIL_SRCS})
