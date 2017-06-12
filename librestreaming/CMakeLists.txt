# Sets the minimum version of CMake required to build your native library.
# This ensures that a certain set of CMake features is available to
# your build.

cmake_minimum_required(VERSION 3.4.1)

# Specifies a library name, specifies whether the library is STATIC or
# SHARED, and provides relative paths to the source code. You can
# define multiple libraries by adding multiple add.library() commands,
# and CMake builds them for you. When you build your app, Gradle
# automatically packages shared libraries with your APK.

MESSAGE(STATUS "This is BINARY dir " ${HELLO_BINARY_DIR})


  add_library( # Specifies the name of the library.
               resrtmp-lib

               # Sets the library as a shared library.
               SHARED

               # Provides a relative path to your source file(s).


               src/main/jni/rtmp/libresrtmp.c
               src/main/jni/rtmp/librtmp/rtmp.c
               src/main/jni/rtmp/librtmp/parseurl.c
               src/main/jni/rtmp/librtmp/log.c

               src/main/jni/rtmp/librtmp/hashswf.c
               src/main/jni/rtmp/librtmp/amf.c

               )



 #dd_library( # Specifies the name of the library.
 #            restreaming-lib

 #            # Sets the library as a shared library.
 #            SHARED

 #            # Provides a relative path to your source file(s).
 #            src/main/jni/restreaming/colorConvert.c
 #            src/main/jni/restreaming/restreaming.c
 #            )

  # Specifies a path to native header files.
  include_directories(src/main/jni/restreaming/)
  include_directories(src/main/jni/rtmp/)
   include_directories(src/main/jni/rtmp/librtmp/)

#配置加载头文件
include_directories(include)
#动态方式加载
#add_library(openssl SHARED IMPORTED )
add_library(ssl SHARED IMPORTED )
add_library(crypto SHARED IMPORTED )

#引入第三方.so库
set_target_properties(crypto PROPERTIES IMPORTED_LOCATION  H:/DuduWorkSpace/DjDemo1/librestreaming/librestreaming/libs/${ANDROID_ABI}/libcrypto.so)
#set_target_properties(openssl PROPERTIES IMPORTED_LOCATION  libs/${ANDROID_ABI}/libcrypto.so)
set_target_properties(ssl PROPERTIES IMPORTED_LOCATION  H:/DuduWorkSpace/DjDemo1/librestreaming/librestreaming/libs/${ANDROID_ABI}/libssl.so)



  #ADD_SUBDIRECTORY(src/main/jni)

  find_library( # Defines the name of the path variable that stores the
                # location of the NDK library.
                log-lib

                # Specifies the name of the NDK library that
                # CMake needs to locate.
                log )

 # Links your native library against one or more other native libraries.
 target_link_libraries( # Specifies the target library.
                         resrtmp-lib
                         crypto
                         ssl
                         # Links the log library to the target library.
                         ${log-lib} )


 #target_link_libraries( # Specifies the target library.
 #                        restreaming-lib
#
 #                        # Links the log library to the target library.
 #                        ${log-lib} )

#add_library( app-glue
#             STATIC
#             ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c )
#
# You need to link static libraries against your shared native library.
#target_link_libraries( native-lib app-glue ${log-lib} )
