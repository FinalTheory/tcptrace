cmake_minimum_required(VERSION 3.3)
project(tcptrace)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 \
    -Wno-format \
    -Wno-macro-redefined\
    -Wno-deprecated-declarations\
    -Wno-sizeof-pointer-memaccess\
    -Wno-tautological-compare")

set(SOURCE_FILES
    flex_bison/filt_parser.c
    flex_bison/filt_parser.h
    flex_bison/filt_scanner.c
    avl.c
    compress.c
    compress.h
    config.h
    dstring.c
    dstring.h
    dyncounter.c
    dyncounter.h
    erf.c
    etherpeek.c
    file_formats.h
    filter.c
    filter.h
    filter_vars.h
    gcache.c
    gcache.h
    ipv6.c
    ipv6.h
    mfiles.c
    mod_collie.c
    mod_collie.h
    mod_http.c
    mod_http.h
    mod_inbounds.c
    mod_inbounds.h
    mod_realtime.c
    mod_realtime.h
    mod_rttgraph.c
    mod_rttgraph.h
    mod_slice.c
    mod_slice.h
    mod_tcplib.c
    mod_tcplib.h
    mod_traffic.c
    mod_traffic.h
    modules.h
    names.c
    netm.c
    netscout.c
    nlanr.c
    ns.c
    output.c
    plotter.c
    pool.c
    pool.h
    poolaccess.c
    print.c
    rexmit.c
    snoop.c
    snprintf_vms.c
    tcpdump.c
    tcpdump.h
    tcptrace.c
    tcptrace.h
    thruput.c
    trace.c
    udp.c
    version.c
    version.h
    base64/base64.c
    base64/base64.h
)

add_definitions(
        -DLOAD_MODULE_HTTP
        -DHTTP_SAFE
        -DHTTP_DUMP_TIMES
        -DLOAD_MODULE_TRAFFIC
        -DLOAD_MODULE_SLICE
        -DLOAD_MODULE_RTTGRAPH
        -DLOAD_MODULE_COLLIE
        -DLOAD_MODULE_REALTIME
        -DGROK_TCPDUMP
        -DYYTEXT_POINTER=1
        -DHAVE_LIBM=1
        -DSTDC_HEADERS=1
        -DHAVE_SYS_TYPES_H=1
        -DHAVE_SYS_STAT_H=1
        -DHAVE_STDLIB_H=1
        -DHAVE_STRING_H=1
        -DHAVE_MEMORY_H=1
        -DHAVE_STRINGS_H=1
        -DHAVE_INTTYPES_H=1
        -DHAVE_STDINT_H=1
        -DHAVE_UNISTD_H=1
        -DSIZEOF_UNSIGNED_LONG_LONG_INT=8
        -DSIZEOF_UNSIGNED_LONG_INT=8
        -DSIZEOF_UNSIGNED_INT=4
        -DSIZEOF_UNSIGNED_SHORT=2
        -DHAVE_FPURGE=1
        -DHAVE_MKSTEMP=1
        -DHAVE_VALLOC=1
        -DHAVE_INET_PTON=1
        -DUSE_LLU=1

        -DBUILT_USER="huangyan13@baidu.com"
        -DBUILT_DATE="2015-10"
        -DBUILT_HOST="MacBookPro"
)

include_directories(.)

add_library(cJSON STATIC cJSON/cJSON.c)

add_executable(tcptrace ${SOURCE_FILES})
target_link_libraries(tcptrace pcap m cJSON)

add_executable(versnum versnum.c)
