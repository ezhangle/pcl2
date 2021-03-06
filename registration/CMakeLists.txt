set(SUBSYS_NAME registration)
set(SUBSYS_DESC "libpcl2_registration: Iterative Closest Point (ICP) registration")
set(SUBSYS_DEPS core)

set(build TRUE)
PCL_SUBSYS_OPTION(build ${SUBSYS_NAME} ${SUBSYS_DESC} ON)
PCL_SUBSYS_DEPEND(build ${SUBSYS_NAME} DEPS ${SUBSYS_DEPS})

#PCL_ADD_DOC(${SUBSYS_NAME})

if(build)
    set(srcs 
        src/fit.cpp
        src/icp.cpp
        src/transform.cpp
       )

    set(incs 
        include/pcl2/registration/correspondence_identification.h
        include/pcl2/registration/fit.h
        include/pcl2/registration/icp.h
        include/pcl2/registration/transform.h
        )
        
    set(impl_incs 
        )

    set(LIB_NAME pcl2_${SUBSYS_NAME})
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
    PCL_ADD_LIBRARY(${LIB_NAME} ${SUBSYS_NAME} ${srcs} ${incs} ${impl_incs})
    PCL_ADD_SSE_FLAGS(${LIB_NAME})
    PCL_MAKE_PKGCONFIG(${LIB_NAME} ${SUBSYS_NAME} "${SUBSYS_DESC}" "" "" "" "" "")

    # Install include files
    PCL_ADD_INCLUDES(${SUBSYS_NAME} "" ${incs})
    PCL_ADD_INCLUDES(${SUBSYS_NAME} impl ${impl_incs})

    #if(BUILD_TESTS)
    #   add_subdirectory(test)
    #endif(BUILD_TESTS)

    #if(BUILD_EXAMPLES)
    #   add_subdirectory(examples)
    #endif(BUILD_EXAMPLES)
endif(build)
