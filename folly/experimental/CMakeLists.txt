#
# Copyright (C) 2017, yumo
#

set(FOLLY_EXPERIMENTAL_SRCS
    AsymmetricMemoryBarrier.cpp
    DynamicParser.cpp
    EnvUtil.cpp
    FunctionScheduler.cpp
    JemallocNodumpAllocator.cpp
    JSONSchema.cpp
    JSONSchemaTester.cpp
    NestedCommandLineApp.cpp
    ProgramOptions.cpp
	#RCUUtils.cpp
    Select64.cpp
    TestUtil.cpp
)
add_library(folly_experimental OBJECT ${FOLLY_EXPERIMENTAL_SRCS})

