cmake_minimum_required(VERSION 3.11)
project(ICEngine C)
set(CMAKE_C_STANDARD 11)

add_compile_definitions(
		$<$<CONFIG:Debug>:_DEBUG>
)

############################################
# MARK: SDL2
############################################
set(SDL2_DIR dependencies/SDL2/cmake)
set(SDL2_ttf_DIR dependencies/SDL2_ttf/cmake)
set(SDL2_mixer_DIR dependencies/SDL2_mixer/cmake)

find_package(SDL2 REQUIRED)
find_package(SDL2_ttf REQUIRED)
find_package(SDL2_mixer REQUIRED)

############################################
# MARK: ENGINE
############################################
# Sources
file(GLOB_RECURSE ICE_SOURCES
        projects/Engine/src/*.c
        projects/Engine/src/*.h)

# Target
add_library(ICE STATIC
        ${ICE_SOURCES}
)

# Linking
target_link_libraries(ICE PRIVATE SDL2::SDL2)
target_link_libraries(ICE PRIVATE SDL2_ttf::SDL2_ttf)
target_link_libraries(ICE PRIVATE SDL2_mixer::SDL2_mixer)

# Public Includes
target_include_directories(ICE PUBLIC
		projects/Engine/src
)

############################################
# MARK: DEMO - 2DWATCH
############################################
# Sources
file(GLOB_RECURSE 2DWATCH_SOURCES
        projects/Games/2DWatch/src/*.h
        projects/Games/2DWatch/src/*.c
)

# Target
add_executable(2DWatch ${2DWATCH_SOURCES})

# Linking
target_link_libraries(2DWatch PRIVATE
		ICE
		SDL2::SDL2main
		SDL2::SDL2
		SDL2_mixer::SDL2_mixer
		SDL2_ttf::SDL2_ttf
)

############################################
# MARK: DEMO - HelloWorld
############################################
# Sources
file(GLOB_RECURSE HelloWorld_SOURCES
		projects/Games/HelloWorld/src/*.h
		projects/Games/HelloWorld/src/*.c
)

# Target
add_executable(HelloWorld ${HelloWorld_SOURCES})

# Linking
target_link_libraries(HelloWorld PRIVATE
		ICE
		SDL2::SDL2main
		SDL2::SDL2
		SDL2_mixer::SDL2_mixer
		SDL2_ttf::SDL2_ttf
)

############################################
# MARK: DEMO - HelloWorld
############################################
# Sources
file(GLOB_RECURSE ICE_GameTemplate1_SOURCES
		projects/Games/ICE_GameTemplate1/src/*.h
		projects/Games/ICE_GameTemplate1/src/*.c
)

# Target
add_executable(ICE_GameTemplate1 ${ICE_GameTemplate1_SOURCES})

# Linking
target_link_libraries(ICE_GameTemplate1 PRIVATE
		ICE
		SDL2::SDL2main
		SDL2::SDL2
		SDL2_mixer::SDL2_mixer
		SDL2_ttf::SDL2_ttf
)

############################################
# MARK: UT - String
############################################
# Sources
file(GLOB_RECURSE UT_STRING_SOURCE
		projects/UT/String/src/*.h
		projects/UT/String/src/*.c
)

# Target
add_executable(UT_STRING ${UT_STRING_SOURCE})

# Linking
target_link_libraries(UT_STRING PRIVATE
		ICE
		SDL2::SDL2main
		SDL2::SDL2
		SDL2_mixer::SDL2_mixer
		SDL2_ttf::SDL2_ttf
)

############################################
# MARK: Tools - Bin2c
############################################
# Sources
file(GLOB_RECURSE BIN2C_SOURCES
		projects/Tools/bin2c/src/*.h
		projects/Tools/bin2c/src/*.c
)

# Target
add_executable(BIN2C ${BIN2C_SOURCES})