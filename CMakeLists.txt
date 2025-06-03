cmake_minimum_required(VERSION 3.26)
project(oop)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

include(cmake/Options.cmake)
include(cmake/CompilerFlags.cmake)
include(cmake/CopyHelper.cmake)

# If building on Windows and you installed SFML somewhere custom, only then set SFML_DIR.
if(WIN32)
    # Change this to wherever you keep SFML on your dev machine:
    set(SFML_DIR "C:/Libraries/SFML-2.5.1/lib/cmake/SFML")
endif()

find_package(SFML 2.5 REQUIRED COMPONENTS graphics window system)

add_executable(oop
        main.cpp
        generated/src/Helper.cpp
        generated/src/Street.cpp
        generated/src/Intersection.cpp
        generated/src/Stoplight.cpp
        generated/src/Utils.cpp
        generated/src/Vehicle.cpp
        generated/src/Simulator.cpp
        generated/src/TrafficSimulationException.cpp
        generated/src/VehicleFactory.cpp
        generated/src/Car.cpp
        generated/src/Bus.cpp
        generated/src/PriorityVehicle.cpp
        generated/src/Behaviour.cpp
        generated/src/CarBehaviour.cpp
        generated/src/BusBehaviour.cpp
        generated/src/PriorityBehaviour.cpp
        generated/src/GraphicSimulator.cpp
)

target_link_libraries(oop PRIVATE sfml-graphics sfml-window sfml-system)

set_compiler_flags(RUN_SANITIZERS TRUE TARGET_NAMES oop)

target_include_directories(oop SYSTEM PRIVATE generated/include)

install(TARGETS oop DESTINATION ${DESTINATION_DIR})
if(APPLE)
    install(FILES launcher.command DESTINATION ${DESTINATION_DIR})
endif()

copy_files(FILES tastatura.txt COPY_TO_DESTINATION TARGET_NAME oop)

