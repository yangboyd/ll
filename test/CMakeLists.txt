include (CTest)

add_executable (init init.c llobj.h)
target_link_libraries (init ll)
add_test (init init)

add_executable (push_front push_front.c llobj.h)
target_link_libraries (push_front ll)
add_test (push_front push_front)

add_executable (push_back push_back.c llobj.h)
target_link_libraries (push_back ll)
add_test (push_back push_back)

add_executable (prev prev.c llobj.h)
target_link_libraries (prev ll)
add_test (prev prev)

add_executable (push push.c llobj.h)
target_link_libraries (push ll)
add_test (push push)

add_executable (repeated_push repeated_push.c llobj.h)
target_link_libraries (repeated_push ll)
add_test (repeated_push repeated_push)

add_executable (remove remove.c llobj.h)
target_link_libraries (remove ll)
add_test (remove remove)

add_executable (remove_ref remove_ref.c llobj.h)
target_link_libraries (remove_ref ll)
add_test (remove_ref remove_ref)

find_package (Threads)
if (Threads_FOUND)
	if (CMAKE_USE_PTHREADS_INIT)
		add_definitions (-DUSE_POSIX_THREADS)
	elseif (CMAKE_USE_WIN32_THREADS_INIT)
		add_definitions (-DUSE_WIN32_THREADS)
	else ()
		set (Threads_FOUND FALSE FORCE)
	endif ()
endif (Threads_FOUND)
if (Threads_FOUND)
	add_definitions (-pthread)

	add_executable (thr_push thr_push.c llobj.h)
	target_link_libraries (thr_push ll ${CMAKE_THREAD_LIBS_INIT})
	add_test (thr_push thr_push)

	add_executable (thr_unlink thr_unlink.c llobj.h)
	target_link_libraries (thr_unlink ll ${CMAKE_THREAD_LIBS_INIT})
	add_test (thr_unlink thr_unlink)
endif (Threads_FOUND)
