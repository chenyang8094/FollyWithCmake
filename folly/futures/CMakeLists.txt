#
# Copyright (C) 2017, yumo
#

set(FOLLY_FUTURES_SRCS
	Barrier.cpp
	Future.cpp
	InlineExecutor.cpp
	ManualExecutor.cpp
	QueuedImmediateExecutor.cpp
	ThreadWheelTimekeeper.cpp
)
add_library(folly_futures OBJECT ${FOLLY_FUTURES_SRCS})
