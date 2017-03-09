#
# Copyright (C) 2017, yumo
#

set(FOLLY_SSL_DETAIL_SRCS
	OpenSSLCertUtils.cpp
	OpenSSLHash.cpp
)
add_library(folly_ssl_detail OBJECT ${FOLLY_SSL_DETAIL_SRCS})
