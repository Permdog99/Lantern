set(CMAKE_CXX_VISIBILITY_PRESET hidden)
set(CMAKE_VISIBILITY_INLINES_HIDDEN 1)

cmake_minimum_required(VERSION 3.30)
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

include(GenerateExportHeader)

add_subdirectory(lib/detours/)

add_library(Lantern SHARED ${SRC_FILES})

include_directories(Lantern PUBLIC ${SRC_FILES})

set_target_properties(Lantern
  PROPERTIES
  DEFINE_SYMBOL "LANTERN_EXPORTS"
)

add_library(Detours ALIAS lib_detours)

target_link_libraries(Lantern PUBLIC Detours)



set(STATIC_SRC_FILES
	resource.h 
	Resource.rc

	lantern/framework.h 
	lantern/LanternMod.h 
	
	lantern/Util/Event.cpp 
	lantern/Util/Event.h 
	lantern/Util/HookHelper.h 
	lantern/Util/Logger.cpp 
	lantern/Util/Logger.h 
)


add_library(Lantern-Lib ${STATIC_SRC_FILES})

include_directories(Lantern-Lib PUBLIC ${STATIC_SRC_FILES})

set_target_properties(Lantern-Lib
  PROPERTIES
  DEFINE_SYMBOL "LANTERN_EXPORTS"
)

target_link_libraries(Lantern-Lib PUBLIC Detours)