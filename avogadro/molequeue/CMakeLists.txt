# Pull in MoleQueue
find_package(MoleQueue REQUIRED NO_MODULE)
include_directories(${MoleQueue_INCLUDE_DIRS})

find_package(Eigen3 REQUIRED)
# Add as "system headers" to avoid warnings generated by them with
# compilers that support that notion.
include_directories(SYSTEM ${EIGEN3_INCLUDE_DIR})

find_package(Qt5Widgets REQUIRED)
find_package(Qt5Network REQUIRED)

set(HEADERS
  batchjob.h
  inputgenerator.h
  inputgeneratordialog.h
  inputgeneratorwidget.h
  molequeuedialog.h
  molequeuemanager.h
  molequeuequeuelistmodel.h
  molequeuewidget.h
)

set(SOURCES
  batchjob.cpp
  inputgenerator.cpp
  inputgeneratordialog.cpp
  inputgeneratorwidget.cpp
  molequeuedialog.cpp
  molequeuemanager.cpp
  molequeuequeuelistmodel.cpp
  molequeuewidget.cpp
)

set(UIS
  inputgeneratordialog.ui
  inputgeneratorwidget.ui
  molequeuedialog.ui
  molequeuewidget.ui
)
qt5_wrap_ui(UI_SOURCES ${UIS})
list(APPEND SOURCES ${UI_SOURCES})

avogadro_add_library(AvogadroMoleQueue ${HEADERS} ${SOURCES})
qt5_use_modules(AvogadroMoleQueue Widgets Network)
set_target_properties(AvogadroMoleQueue PROPERTIES AUTOMOC TRUE)
target_link_libraries(AvogadroMoleQueue AvogadroQtGui MoleQueueClient)