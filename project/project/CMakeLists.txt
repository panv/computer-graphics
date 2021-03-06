# the exercise name is nothing else than the directory
get_filename_component(EXERCISENAME ${CMAKE_CURRENT_LIST_DIR} NAME)
file(GLOB_RECURSE SOURCES "*.cpp")
file(GLOB_RECURSE HEADERS "*.h")

# these files are copied only once
file(GLOB TEXTURES
    skybox/*.jpg
    skybox/*.tga
    skybox/*.png
    terrain/*.jpg
    terrain/*.png)
copy_files_once(${TEXTURES})

file(COPY points.txt DESTINATION build/project/points.txt)

# list all the files you want to copy everytime
# you build (ie, you want the shaders there)
file(GLOB SHADERS
  skybox/*.glsl
  terrain/*.glsl
  screenquad/*.glsl
  perlin/*.glsl
  water/*.glsl)

deploy_shaders_to_build_dir(${SHADERS})

add_executable(${EXERCISENAME} ${SOURCES} ${HEADERS} ${SHADERS})
target_link_libraries(${EXERCISENAME} ${COMMON_LIBS})
