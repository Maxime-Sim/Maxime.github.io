find_package(SFML COMPONENTS system window graphics audio CONFIG REQUIRED)
find_package(IMGUI-SFML COMPONENTS system window graphics audio CONFIG REQUIRED)

# Obtenez tous les fichiers source
file(GLOB ALL_SRC "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")

# Créez l'exécutable à partir des sources
add_executable(${PROJECT_NAME} ${ALL_SRC} "CMake.cpp")

# Inclure le répertoire des fichiers d'en-tête
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/include)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET Cmake PROPERTY CXX_STANDARD 20)
endif()

# Créer la bibliothèque Console
add_library(Console STATIC "${CMAKE_CURRENT_SOURCE_DIR}/lib/Console.cpp")

# Inclure le répertoire des fichiers d'en-tête de la bibliothèque Console
target_include_directories(Console PUBLIC ${CMAKE_SOURCE_DIR}/include)

# Lier la bibliothèque Console à votre projet
target_link_libraries(${PROJECT_NAME} PUBLIC Console)

# TODO : Ajoutez des tests et installez des cibles si nécessaire

target_link_libraries(${PROJECT_NAME} PRIVATE 
    sfml-audio
    sfml-system
    sfml-graphics
    sfml-window
    sfml-network
)