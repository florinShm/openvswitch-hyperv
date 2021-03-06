IF(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
include_directories("$ENV{INCLUDE}")
include_directories("${CMAKE_SOURCE_DIR}")
include_directories("${OVS_Port_SOURCE_DIR}/windows")
include_directories("${OVS_Port_SOURCE_DIR}/windows/thirdparty/win-pthread/include")
link_directories("${OVS_Port_SOURCE_DIR}/windows")
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
include_directories("${OVS_Port_SOURCE_DIR}")
include_directories("${OVS_Port_SOURCE_DIR}/include")
include_directories("${OVS_Port_SOURCE_DIR}/lib")
include_directories("${OVS_Port_SOURCE_DIR}/ofproto")
include_directories("${OVS_Port_SOURCE_DIR}/ovsdb")
include_directories("${OVS_Port_SOURCE_DIR}/generated")

IF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
set (flags_openvswitch "-Wstrict-prototypes -Wall -Wno-sign-compare -Wpointer-arith -Wdeclaration-after-statement -Wformat-security -Wswitch-enum -Wunused-parameter -Wstrict-aliasing -Wbad-function-cast -Wcast-align -Wstrict-prototypes -Wold-style-definition -Wmissing-prototypes -Wmissing-field-initializers -Wno-override-init  -g ")
set(CMAKE_C_FLAGS  "${flags_openvswitch}" )
set(CMAKE_C_ARCHIVE_CREATE "<CMAKE_AR> cru <LINK_FLAGS> <TARGET> <OBJECTS>")
set(CMAKE_C_ARCHIVE_FINISH "<CMAKE_RANLIB> <TARGET>")
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

set ( sources_openvswitch 
aes128.c
bond.c
backtrace.c
bitmap.c
bundle.c
byteq.c
cfm.c
classifier.c
command-line.c
coverage.c
csum.c
daemon.c
dirs.c 
dpif-linux.c
dpif-netdev.c
dpif.c
dummy.c
dynamic-string.c
entropy.c
fatal-signal.c
flow.c
hash.c
heap.c
hmap.c
hmapx.c
jhash.c
json.c
jsonrpc.c
lacp.c
leak-checker.c
learn.c
learning-switch.c
list.c
lockfile.c
mac-learning.c
match.c
memory.c
meta-flow.c
multipath.c
netdev-dummy.c
netdev-linux.c
netdev-vport.c
netdev.c
netlink-notifier.c
netlink-socket.c
netlink.c
nx-match.c
odp-util.c
ofp-actions.c
ofp-errors.c
ofp-msgs.c
ofp-parse.c
ofp-print.c
ofp-util.c
ofp-version-opt.c
ofpbuf.c
ovsdb-data.c
ovsdb-error.c
ovsdb-idl.c
ovsdb-parser.c
ovsdb-types.c
packets.c
pcap-file.c
poll-loop.c
process.c
random.c
rconn.c
reconnect.c
route-table.c
rtnetlink-link.c
sha1.c
shash.c
signals.c
simap.c
smap.c
socket-util.c
sort.c
sset.c
stp.c
stream-fd.c
stream-nossl.c
stream-tcp.c
stream-unix.c
stream.c
stress.c
string.c
svec.c
table.c
tag.c
timer.c
timeval.c
token-bucket.c
unicode.c
unixctl.c
util.c
uuid.c
vconn-stream.c
vconn.c
vlan-bitmap.c
vlandev.c
vlog.c
vswitch-idl.c
worker.c 
Socket.c )

list(SORT sources_openvswitch)
add_library (openvswitch ${sources_openvswitch})

IF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
set (flags_sflow "-Wstrict-prototypes -Wall -Wno-sign-compare -Wpointer-arith -Wdeclaration-after-statement -Wformat-security -Wswitch-enum -Wunused-parameter -Wstrict-aliasing -Wbad-function-cast -Wcast-align -Wstrict-prototypes -Wold-style-definition -Wmissing-prototypes -Wmissing-field-initializers -Wno-override-init  -Wno-unused -Wno-unused-parameter")
set(CMAKE_C_FLAGS  "${flags_sflow}" )
set(CMAKE_C_ARCHIVE_CREATE "<CMAKE_AR> cru <LINK_FLAGS> <TARGET> <OBJECTS>")
set( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${GCC_COVERAGE_LINK_FLAGS}" )
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

set (sources_sflow sflow_agent.c sflow_poller.c sflow_receiver.c sflow_sampler.c)
add_library (sflow ${sources_sflow})

