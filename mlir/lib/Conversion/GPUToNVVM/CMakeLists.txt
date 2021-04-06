set(LLVM_TARGET_DEFINITIONS GPUToNVVM.td)
mlir_tablegen(GPUToNVVM.cpp.inc -gen-rewriters)
add_public_tablegen_target(MLIRGPUToNVVMIncGen)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

add_mlir_conversion_library(MLIRGPUToNVVMTransforms
  LowerGpuOpsToNVVMOps.cpp

  DEPENDS
  MLIRConversionPassIncGen
  MLIRGPUToNVVMIncGen

  LINK_LIBS PUBLIC
  MLIRGPU
  MLIRLLVMIR
  MLIRNVVMIR
  MLIRPass
  MLIRStandardToLLVM
  MLIRTransformUtils
  )
