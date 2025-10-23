cmake_minimum_required(VERSION 3.15)
project(nuc_video_mesh)

set(CMAKE_CXX_STANDARD 17)

# Include directories
include_directories(src src/utils src/services)

# Source files
file(GLOB SOURCES
    "src/*.cpp"
    "src/utils/*.cpp"
    "src/services/*.cpp"
)


# Find required packages
find_package(Boost REQUIRED COMPONENTS system thread)
find_package(OpenCV REQUIRED)
find_package(PkgConfig REQUIRED)
pkg_check_modules(ZMQ REQUIRED libzmq)
find_library(ISAL_LIBRARY isal)
find_package(SQLite3 REQUIRED)
find_package(CURL REQUIRED)

# Executable
add_executable(nuc_video_mesh ${SOURCES})

# Optional: link external libraries
# Link all the libraries
target_link_libraries(nuc_video_mesh
    Boost::system
    Boost::thread
    ${OpenCV_LIBS}
    ${ZMQ_LIBRARIES}
    ${ISAL_LIBRARY}
    SQLite::SQLite3
    CURL::libcurl
)