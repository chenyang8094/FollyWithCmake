#
# Copyright (C) 2017, yumo
#

set(FOLLY_PROTABILITY_SRCS
	BitsFunctexcept.cpp
	Builtins.cpp
	Dirent.cpp
	Fcntl.cpp
	Libgen.cpp
	Malloc.cpp
	Memory.cpp
	OpenSSL.cpp
	Sockets.cpp
	Stdio.cpp
	Stdlib.cpp
	String.cpp
	SysFile.cpp
	SysMembarrier.cpp
	SysMman.cpp
	SysResource.cpp
	SysStat.cpp
	SysTime.cpp
	SysUio.cpp
	Time.cpp
	Unistd.cpp
)
add_library(folly_portability OBJECT ${FOLLY_PROTABILITY_SRCS})
