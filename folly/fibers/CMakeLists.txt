#
# Copyright (C) 2017, yumo
#

set(FOLLY_FIBERS_SRCS
    Baton.cpp
	Fiber.cpp
	FiberManager.cpp
	FiberManagerMap.cpp
	GuardPageAllocator.cpp
	Semaphore.cpp
	TimeoutController.cpp
)
add_library(folly_fibers OBJECT ${FOLLY_FIBERS_SRCS})
