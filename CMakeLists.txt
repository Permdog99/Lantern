include(FetchContent)

set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)

cmake_minimum_required(VERSION 3.8.2)
project(Lantern)
set (CMAKE_CXX_STANDARD 20)

set(SRC_FILES
	resource.h 
	Resource.rc

	lantern/pch.h 
	lantern/pch.cpp 
	lantern/framework.h 
	lantern/Lantern.cpp 
	lantern/Lantern.h 
	lantern/LanternMod.h 
	
	lantern/Util/Event.cpp 
	lantern/Util/Event.h 
	lantern/Util/HookHelper.h 
	lantern/Util/Logger.cpp 
	lantern/Util/Logger.h 

	lantern/InternalHooks/Minecraft.cpp 
	lantern/InternalHooks/Minecraft.h
)

# Safetyhook
FetchContent_Declare(
safetyhook
    GIT_REPOSITORY "https://github.com/cursey/safetyhook.git"
    GIT_TAG "origin/main"
)

FetchContent_MakeAvailable(safetyhook)

include_directories(lantern)

add_library(Lantern SHARED ${SRC_FILES})
target_link_libraries(Lantern PUBLIC safetyhook)

include(GenerateExportHeader)
generate_export_header(Lantern)
set_target_properties(Lantern
  PROPERTIES
  DEFINE_SYMBOL "LANTERN_EXPORTS"
  )

