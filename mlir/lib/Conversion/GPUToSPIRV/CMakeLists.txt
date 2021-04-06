set(LLVM_TARGET_DEFINITIONS GPUToSPIRV.td)
mlir_tablegen(GPUToSPIRV.cpp.inc -gen-rewriters)
add_public_tablegen_target(MLIRGPUToSPIRVIncGen)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_mlir_conversion_library(MLIRGPUToSPIRVTransforms
  ConvertGPUToSPIRV.cpp
  ConvertGPUToSPIRVPass.cpp

  DEPENDS
  MLIRConversionPassIncGen
  MLIRGPUToSPIRVIncGen

  LINK_LIBS PUBLIC
  MLIRGPU
  MLIRIR
  MLIRPass
  MLIRSCFToSPIRV
  MLIRSPIRV
  MLIRStandardOps
  MLIRStandardToSPIRVTransforms
  MLIRSupport
  MLIRTransforms
  )
