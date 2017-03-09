#
# Copyright (C) 2017, yumo
#

set(FOLLY_SSL_SRCS
	OpenSSLCertUtils.cpp
	OpenSSLHash.cpp
)
add_library(folly_ssl OBJECT ${FOLLY_SSL_SRCS})
