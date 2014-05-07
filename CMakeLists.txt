cmake_minimum_required(VERSION 2.8.9)


#-----------------------------------------------------------------------------
if(NOT Slicer_SOURCE_DIR)
set(EXTENSION_NAME SurfaceReconstruction)
set(EXTENSION_HOMEPAGE "http://wiki.slicer.org/slicerWiki/index.php/Documentation/Nightly/Extensions/SurfaceReconstruction")
set(EXTENSION_CATEGORY "Surface Models")
set(EXTENSION_CONTRIBUTORS "Chenxi-Zhang David-Doria Arnaud-Gelas Michael-Kazhdan Matthew-Bolitho Hugues-Hoppe Jean-Christophe Fillion-Robin (Kitware)")
set(EXTENSION_DESCRIPTION "This is an implementation of the Poisson surface reconstruction algorithm in the VTK framework")
set(EXTENSION_ICONURL "http://wiki.slicer.org/slicerWiki/images/c/cf/SurfaceReconstruction.png")
endif()

#-----------------------------------------------------------------------------
set(MODULE_NAME SurfaceReconstruction)
#-----------------------------------------------------------------------------
if(NOT Slicer_SOURCE_DIR)
find_package(Slicer REQUIRED)
include(${Slicer_USE_FILE})
endif()

#-----------------------------------------------------------------------------
set(MODULE_TARGET_LIBRARIES
  ${ITK_LIBRARIES}
  ${VTK_LIBRARIES}
  )

#-----------------------------------------------------------------------------
SEMMacroBuildCLI(
  NAME ${MODULE_NAME}
  ADDITIONAL_SRCS
	vtkPoissonReconstruction.cxx 
	Factor.cpp 
	Geometry.cpp 
	MarchingCubes.cpp 
	MultiGridOctest.cpp 
	MultiGridOctreeData.cpp
  TARGET_LIBRARIES ${MODULE_TARGET_LIBRARIES}
  )


#-----------------------------------------------------------------------------
if(BUILD_TESTING)
  add_subdirectory(Testing)
endif()


#-----------------------------------------------------------------------------
if(NOT Slicer_SOURCE_DIR)
  include(${Slicer_EXTENSION_CPACK})
endif()