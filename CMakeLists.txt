project(pocl-build)
cmake_minimum_required(VERSION 3.6)

file(DOWNLOAD
	"http://llvm.org/releases/3.8.1/llvm-3.8.1.src.tar.xz"
	"${CMAKE_CURRENT_LIST_DIR}/llvm.tar.xz")

execute_process(COMMAND tar xJf llvm.tar.xz)

#file(DOWNLOAD http://llvm.org/releases/3.8.1/cfe-3.8.1.src.tar.xz cfe.tar.xz)
