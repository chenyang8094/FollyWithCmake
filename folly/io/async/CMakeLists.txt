#
# Copyright (C) 2017, yumo
#

set(FOLLY_IO_ASYNC_SRCS
	AsyncPipe.cpp
	AsyncServerSocket.cpp
	AsyncSignalHandler.cpp
	AsyncSocket.cpp
	AsyncSSLSocket.cpp
	AsyncTimeout.cpp
	AsyncUDPSocket.cpp
	EventBase.cpp
	EventBaseLocal.cpp
	EventBaseManager.cpp
	EventBaseThread.cpp
	EventHandler.cpp
	HHWheelTimer.cpp
	Request.cpp
	ScopedEventBaseThread.cpp
	SSLContext.cpp
	TimeoutManager.cpp
	VirtualEventBase.cpp
)
add_library(folly_io_async OBJECT ${FOLLY_IO_ASYNC_SRCS})
