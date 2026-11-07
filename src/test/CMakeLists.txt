# ---- portal engine tests ----

add_executable(portal_test
    main.c
    test_arith.c
    test_map.c
    test_mode5.c
    test_palette.c
    test_render.c
    test_sprite.c
    testmaps.c
    probes/probe_collision.c
    probes/probe_fan.c
    probes/probe_walk.c
)

target_link_libraries(portal_test PRIVATE portal)

if(MSVC)
    target_compile_options(portal_test PRIVATE /W3)
else()
    target_compile_options(portal_test PRIVATE -Wall -Wextra)
endif()

# run the tests as a post-build step, richc style
add_custom_command(
    TARGET portal_test POST_BUILD
    COMMAND $<TARGET_FILE:portal_test>
    WORKING_DIRECTORY $<TARGET_FILE_DIR:portal_test>
    COMMENT "Running portal tests"
    VERBATIM
)
