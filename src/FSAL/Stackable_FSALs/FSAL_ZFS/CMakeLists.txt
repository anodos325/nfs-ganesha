add_definitions(
  -D__USE_GNU
  -D_GNU_SOURCE
)

set( LIB_PREFIX 64)

########### next target ###############

SET(fsalzfs_LIB_SRCS
   handle.c
   file.c
   xattrs.c
   zfs_methods.h
   main.c
   export.c
)

add_library(fsalzfs MODULE ${fsalzfs_LIB_SRCS})
add_sanitizers(fsalzfs)

target_link_libraries(fsalzfs
  ganesha_nfsd
  "-Wl,--no-undefined"
)

set_target_properties(fsalzfs PROPERTIES VERSION 4.2.0 SOVERSION 4)
install(TARGETS fsalzfs COMPONENT fsal DESTINATION ${FSAL_DESTINATION} )

########### install files ###############
