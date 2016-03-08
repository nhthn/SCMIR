#cmake -DCMAKE_OSX_ARCHITECTURES='i386;x86_64' ..

cmake_minimum_required (VERSION 2.6)
project (SCMIRexecutables)

add_executable(noveltycurve noveltycurve/noveltycurve.cpp)
add_executable(similaritymatrix similaritymatrix/similarity.cpp)

include_directories(${LIBGSL_PATH})

file(GLOB gmmSources gmm/*cpp)
add_executable(gmm ${gmmSources})

file(GLOB hmmSources hmm/*cpp)
add_executable(hmm ${hmmSources})

target_link_libraries(gmm ${LIBGSL_PATH}/libgsl.a ${LIBGSL_PATH}/libgslcblas.a)

file(GLOB nnSources NeuralNet/*cpp)
add_executable(NeuralNet ${nnSources})

INSTALL(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/noveltycurve ${CMAKE_CURRENT_BINARY_DIR}/similaritymatrix ${CMAKE_CURRENT_BINARY_DIR}/NeuralNet ${CMAKE_CURRENT_BINARY_DIR}/hmm ${CMAKE_CURRENT_BINARY_DIR}/gmm DESTINATION "${CMAKE_CURRENT_SOURCE_DIR}/../SCMIRExtensions/scmirexec/")
