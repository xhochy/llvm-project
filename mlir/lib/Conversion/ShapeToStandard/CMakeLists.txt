set(LLVM_TARGET_DEFINITIONS ShapeToStandardPatterns.td)
mlir_tablegen(ShapeToStandardPatterns.inc -gen-rewriters)
add_public_tablegen_target(ShapeToStandardPatternsIncGen)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
add_mlir_conversion_library(MLIRShapeToStandard
  ShapeToStandard.cpp

  ADDITIONAL_HEADER_DIRS
  ${MLIR_MAIN_INCLUDE_DIR}/mlir/Conversion/ShapeToStandard

  DEPENDS
  MLIRConversionPassIncGen
  ShapeToStandardPatternsIncGen

  LINK_COMPONENTS
  Core

  LINK_LIBS PUBLIC
  MLIREDSC
  MLIRIR
  MLIRShape
  MLIRPass
  MLIRSCF
  MLIRTransforms
  )
