project (CMA-ES)
cmake_minimum_required( VERSION 3.0.2 )

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
find_package(Eigen)
find_package(Boost REQUIRED python)
find_package(PythonLibs)
find_package(Numpy)
find_package(Glog)

include_directories(${EIGEN_INCLUDE_DIR})
include_directories(${GLOG_INCLUDE_DIR})
add_definitions(-DHAVE_GLOG=1)
add_library(cmaes
    src/ipopcmastrategy.cc
    src/ipopcmastrategy.h
    src/llogging.h
    src/noboundstrategy.h
    src/opti_err.h
    src/parameters.h
    src/pli.h
    src/pwq_bound_strategy.cc
    src/pwq_bound_strategy.h
    src/scaling.h
    src/surrcmaes.h
    src/surrogatestrategy.cc
    src/surrogatestrategy.h
    src/vdcmaupdate.cc
    src/vdcmaupdate.h
    src/acovarianceupdate.cc
    src/acovarianceupdate.h
    src/bipopcmastrategy.cc
    src/bipopcmastrategy.h
    src/candidate.h
    src/cmaes.h
    src/cmaparameters.cc
    src/cmaparameters.h
    src/cmasolutions.cc
    src/cmasolutions.h
    src/cmastopcriteria.cc
    src/cmastopcriteria.h
    src/cmastrategy.cc
    src/cmastrategy.h
    src/contour.h
    src/covarianceupdate.cc
    src/covarianceupdate.h
    src/eigenmvn.h
    src/eo_matrix.h
    src/errstats.cc
    src/errstats.h
    src/esoptimizer.h
    src/esostrategy.cc
    src/esostrategy.h
    src/genopheno.h
    src/surrogates/rsvm_surr_strategy.hpp
    src/surrogates/rankingsvm.hpp)

include_directories(./src)
include_directories(${PYTHON_NUMPY_INCLUDE_DIR})
include_directories(${PYTHON_INCLUDE_DIRS})
include_directories(${Boost_INCLUDE_DIRS})

add_library(lcmaes SHARED
	python/py_boost_function.hpp
	python/lcmaes.cc)
target_link_libraries(lcmaes cmaes ${Boost_LIBRARIES} ${PYTHON_LIBRARIES} ${GLOG_LIBRARY})
set_target_properties(lcmaes PROPERTIES PREFIX "")
set_target_properties(lcmaes PROPERTIES SUFFIX ".pyd")