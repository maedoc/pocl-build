project(pocl-build)
cmake_minimum_required(VERSION 3.6)
include("cmake_util.cmake")

# pick versions
set(LLVM_VER "3.8.1")
set(POCL_VER "0.13")
MESSAGE("Using LLVM verion ${LLVM_VER} and PoCL version ${POCL_VER}.")

# get LLVM sources
foreach(llvm_proj "llvm" "cfe")
	get_source_archive(
		"http://llvm.org/releases/${LLVM_VER}/${llvm_proj}-${LLVM_VER}.src.tar.xz"
		"${llvm_proj}-${LLVM_VER}.src.tar.xz")
endforeach(llvm_proj)

# get PortableCL source
get_source_archive(
	"http://portablecl.org/downloads/pocl-${POCL_VER}.tar.gz"
	"pocl-${POCL_VER}.tar.gz")

# unpack archives

foreach(srcdir "cfe-${LLVM_VER}.src" "llvm-${LLVM_VER}.src" "pocl-${POCL_VER}")
	unpack_source(${srcdir})
endforeach(srcdir)

#file(DOWNLOAD http://llvm.org/releases/3.8.1/cfe-3.8.1.src.tar.xz cfe.tar.xz)
