#
# Copyright (C) 2017, yumo
#

set(FOLLY_IO_ASYNC_SSL_SRCS
	OpenSSLUtils.cpp
	SSLErrors.cpp
)
add_library(folly_io_async_ssl OBJECT ${FOLLY_IO_ASYNC_SSL_SRCS})
