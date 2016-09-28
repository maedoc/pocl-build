project(pocl-build)
cmake_minimum_required(VERSION 3.6)
include("pocl_build_util.cmake")
include(ExternalProject)

# pick versions
set(LLVM_VER "3.8.1")
set(POCL_VER "0.13")
MESSAGE("Using LLVM verion ${LLVM_VER} and PoCL version ${POCL_VER}.")

# setup as external projects
ExternalProject_Add(llvm
	PREFIX "llvm"
	URL "http://llvm.org/releases/${LLVM_VER}/llvm-${LLVM_VER}.src.tar.xz"
	INSTALL_DIR "$ENV{PREFIX}"
	CMAKE_CACHE_ARGS
		-DBUILD_SHARED_LIBS:BOOL=OFF
		-DLLVM_ENABLE_RTTI:BOOL=ON
		-DLLVM_TARGETS_TO_BUILD:STRING=X86
)

ExternalProject_Add(cfe
	DEPENDS llvm
	PREFIX "cfe"
	URL "http://llvm.org/releases/${LLVM_VER}/cfe-${LLVM_VER}.src.tar.xz"
	INSTALL_DIR "$ENV{PREFIX}"
	CMAKE_CACHE_ARGS
		-DCLANG_TOOL_LIBCLANG_BUILD:BOOL=ON
		-DLIBCLANG_BUILD_STATIC:BOOL=ON
		-DLLVM_ENABLE_RTTI:BOOL=ON
)

ExternalProject_Add(pocl
	DEPENDS llvm cfe
	PREFIX "pocl"
	URL "http://portablecl.org/downloads/pocl-${POCL_VER}.tar.gz"
	INSTALL_DIR "$ENV{PREFIX}"
	CMAKE_CACHE_ARGS
		-DBUILD_SHARED_LIBS:BOOL=ON
		-DENABLE_ICD:BOOL=ON
		-DDIRECT_LINKAGE:BOOL=OFF
		-DINSTALL_OPENCL_HEADERS:BOOL=OFF
		-DPOCL_DEBUG_MESSAGES:BOOL=ON
		-DSTATIC_LLVM:BOOL=OFF
		-DKERNELLIB_HOST_CPU_VARIANTS:STRING=distro
)
