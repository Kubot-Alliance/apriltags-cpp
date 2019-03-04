add_library(apriltags-cpp
  CameraUtil.cpp
  DebugImage.cpp
  Geometry.cpp 
  GrayModel.cpp
  MathUtil.cpp 
  Refine.cpp
  TagDetector.cpp 
  TagFamily.cpp
  TagFamilies.cpp
  UnionFindSimple.cpp
)

set(AT_LIBS apriltags-cpp ${OPENCV_LDFLAGS})

add_executable(camtest camtest.cpp)
target_link_libraries(camtest ${AT_LIBS})

add_executable(tagtest tagtest.cpp)
target_link_libraries(tagtest ${AT_LIBS})

add_executable(quadtest quadtest.cpp)
target_link_libraries(quadtest ${AT_LIBS})

if (GLUT_LIBRARY)

  add_executable(gltest gltest.cpp)
  target_link_libraries(gltest ${GLUT_LIBRARY} ${OPENGL_LIBRARY} ${AT_LIBS})

endif()

if (CAIRO_FOUND)

  add_executable(maketags maketags.cpp)
  target_link_libraries(maketags ${CAIRO_LIBRARIES} ${AT_LIBS} ${CAIRO_LIBS})

endif()

INSTALL(TARGETS apriltags-cpp
        ARCHIVE DESTINATION lib)
INSTALL(FILES
        AprilTypes.h
        CameraUtil.h
        DebugImage.h
        Geometry.h
        GrayModel.h
        MathUtil.h
        Profiler.h
        Refine.h
        TagDetection.h
        TagDetector.h
        TagFamily.h
        UnionFindSimple.h
        DESTINATION include/apriltags-cpp)
