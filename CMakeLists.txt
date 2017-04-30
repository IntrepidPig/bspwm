cmake_minimum_required(VERSION 3.7)
project(bspwm)

set(CMAKE_CXX_STANDARD 11)

execute_process(
		COMMAND bash -c "git describe | xargs echo -n"
		OUTPUT_VARIABLE BSPWM_VERSION
)

message(STATUS ${BSPWM_VERSION})

add_definitions(-DVERSION="${BSPWM_VERSION}")

set(WM_LIBRARIES
		xcb
		xcb-util
		xcb-keysyms
		xcb-icccm
		xcb-ewmh
		xcb-randr
		xcb-xinerama)

set(WM_SOURCE_FILES
		src/bspwm.c
		src/desktop.c
		src/events.c
		src/ewmh.c
		src/geometry.c
		src/helpers.c
		src/history.c
		src/jsmn.c
		src/messages.c
		src/monitor.c
		src/parse.c
		src/pointer.c
		src/query.c
		src/restore.c
		src/rule.c
		src/settings.c
		src/stack.c
		src/subscribe.c
		src/tree.c
		src/window.c)

add_executable(bspwm ${WM_SOURCE_FILES})
target_link_libraries(bspwm ${WM_LIBRARIES})

set(CLI_SOURCE_FILES
		src/bspc.c
		src/helpers.c)

add_executable(bspc ${CLI_SOURCE_FILES})