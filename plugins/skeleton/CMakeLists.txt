PROJECT (skeleton)
# A list of source files
SET(PROJECT_SRCS
    skeleton.cpp
)
# A list of headers
SET(PROJECT_HDRS
    skeleton.h
)
SET_SOURCE_FILES_PROPERTIES( ${PROJECT_HDRS} PROPERTIES HEADER_FILE_ONLY TRUE)

# mash them together (headers are marked as headers and nothing will try to compile them)
LIST(APPEND PROJECT_SRCS ${PROJECT_HDRS})

# option to use a thread for no particular reason
OPTION(SKELETON_THREAD "Use threads in the skeleton plugin." ON)
#linux
IF(UNIX)
    add_definitions(-DLINUX_BUILD)
    SET(PROJECT_LIBS
        # add any extra linux libs here
        ${PROJECT_LIBS}
    )
# windows
ELSE(UNIX)
    SET(PROJECT_LIBS
        # add any extra linux libs here
        ${PROJECT_LIBS}
        $(NOINHERIT)
    )
ENDIF(UNIX)
# this makes sure all the stuff is put in proper places and linked to dfhack
DFHACK_PLUGIN(skeleton ${PROJECT_SRCS} LINK_LIBRARIES ${PROJECT_LIBS})
