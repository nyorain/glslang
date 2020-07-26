project('glslang', ['cpp', 'c'],
	meson_version: '>=0.51',
	default_options: [
		'cpp_std=c++11',
		'c_std=c11',
  		'warning_level=3',
  		'werror=false'])

sources = files(
  'SPIRV/GlslangToSpv.cpp',
  'SPIRV/InReadableOrder.cpp',
  'SPIRV/Logger.cpp',
  'SPIRV/SPVRemapper.cpp',
  'SPIRV/SpvBuilder.cpp',
  'SPIRV/SpvPostProcess.cpp',
  'SPIRV/SpvTools.cpp',
  'SPIRV/disassemble.cpp',
  'SPIRV/doc.cpp',
  'SPIRV/spirv.hpp',
  'glslang/GenericCodeGen/CodeGen.cpp',
  'glslang/GenericCodeGen/Link.cpp',
  'glslang/MachineIndependent/Constant.cpp',
  'glslang/MachineIndependent/InfoSink.cpp',
  'glslang/MachineIndependent/Initialize.cpp',
  'glslang/MachineIndependent/IntermTraverse.cpp',
  'glslang/MachineIndependent/Intermediate.cpp',
  'glslang/MachineIndependent/ParseContextBase.cpp',
  'glslang/MachineIndependent/ParseHelper.cpp',
  'glslang/MachineIndependent/PoolAlloc.cpp',
  'glslang/MachineIndependent/RemoveTree.cpp',
  'glslang/MachineIndependent/Scan.cpp',
  'glslang/MachineIndependent/ShaderLang.cpp',
  'glslang/MachineIndependent/SymbolTable.cpp',
  'glslang/MachineIndependent/Versions.cpp',
  'glslang/MachineIndependent/attribute.cpp',
  'glslang/MachineIndependent/glslang_tab.cpp',
  'glslang/MachineIndependent/intermOut.cpp',
  'glslang/MachineIndependent/iomapper.cpp',
  'glslang/MachineIndependent/limits.cpp',
  'glslang/MachineIndependent/linkValidate.cpp',
  'glslang/MachineIndependent/localintermediate.h',
  'glslang/MachineIndependent/parseConst.cpp',
  'glslang/MachineIndependent/preprocessor/Pp.cpp',
  'glslang/MachineIndependent/preprocessor/PpAtom.cpp',
  'glslang/MachineIndependent/preprocessor/PpContext.cpp',
  'glslang/MachineIndependent/preprocessor/PpScanner.cpp',
  'glslang/MachineIndependent/preprocessor/PpTokens.cpp',
  'glslang/MachineIndependent/propagateNoContraction.cpp',
  'glslang/MachineIndependent/reflection.cpp',
  'glslang/OSDependent/osinclude.h',
)

headers = files(
  'glslang/MachineIndependent/preprocessor/PpTokens.h',
  'glslang/MachineIndependent/propagateNoContraction.h',
  'glslang/MachineIndependent/reflection.h',
  'glslang/Public/ShaderLang.h',
  'glslang/MachineIndependent/glslang_tab.cpp.h',
  'glslang/MachineIndependent/iomapper.h',
  'glslang/MachineIndependent/parseVersions.h',
  'glslang/MachineIndependent/preprocessor/PpContext.h',
  'glslang/MachineIndependent/ScanContext.h',
  'glslang/MachineIndependent/SymbolTable.h',
  'glslang/MachineIndependent/Versions.h',
  'glslang/MachineIndependent/attribute.h',
  'glslang/MachineIndependent/gl_types.h',
  'glslang/MachineIndependent/Scan.h',
  'glslang/Include/BaseTypes.h',
  'glslang/Include/Common.h',
  'glslang/Include/ConstantUnion.h',
  'glslang/Include/InfoSink.h',
  'glslang/Include/InitializeGlobals.h',
  'glslang/Include/PoolAlloc.h',
  'glslang/Include/ResourceLimits.h',
  'glslang/Include/ShHandle.h',
  'glslang/Include/Types.h',
  'glslang/Include/arrays.h',
  'glslang/Include/intermediate.h',
  'glslang/MachineIndependent/Initialize.h',
  'glslang/MachineIndependent/LiveTraverser.h',
  'glslang/MachineIndependent/ParseHelper.h',
  'glslang/MachineIndependent/RemoveTree.h',
  'SPIRV/NonSemanticDebugPrintf.h',
  'SPIRV/SpvBuilder.h',
  'SPIRV/SPVRemapper.h',
  'SPIRV/SpvTools.h',
  'SPIRV/bitutils.h',
  'SPIRV/disassemble.h',
  'SPIRV/doc.h',
  'SPIRV/hex_float.h',
  'SPIRV/spvIR.h',
  'SPIRV/GLSL.ext.AMD.h',
  'SPIRV/GLSL.ext.EXT.h',
  'SPIRV/GLSL.ext.KHR.h',
  'SPIRV/GLSL.ext.NV.h',
  'SPIRV/GLSL.std.450.h',
  'SPIRV/GlslangToSpv.h',
  'SPIRV/Logger.h',
)

inc = include_directories('.')
args = []
if target_machine.system() == 'windows'
	sources += files('glslang/OSDependent/Windows/ossource.cpp')
	args += '-DGLSLANG_OSINCLUDE_WIN32'
else
	sources += files('glslang/OSDependent/Unix/ossource.cpp')
    args += '-DGLSLANG_OSINCLUDE_UNIX'
endif

build_info_py = files('build_info.py')
build_info_h = custom_target(
	'build_info.h',
	output: 'build_info.h',
	input: 'build_info.h.tmpl',
	command: [build_info_py, meson.current_source_dir(), '-i', '@INPUT@', '-o', '@OUTPUT@'])

lib_glslang = library('glslang',
	[sources, build_info_h],
	include_directories: inc,
	dependencies: dependency('threads'),
	cpp_args: args)

dep_glslang = declare_dependency(
	link_with: lib_glslang,
	include_directories: inc,
)
