#
# Copyright (C) 2017, yumo
#

set(FOLLY_IO_SRCS
	Compression.cpp
	Cursor.cpp
	IOBuf.cpp
	IOBufQueue.cpp
	RecordIO.cpp
	ShutdownSocketSet.cpp
)
add_library(folly_io OBJECT ${FOLLY_IO_SRCS})
