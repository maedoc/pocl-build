project(pocl-build)
cmake_minimum_required(VERSION 3.6)

set(LLVM_VER "3.8.1")
set(POCL_VER "0.13")
MESSAGE("Using LLVM verion ${LLVM_VER} and PoCL version ${POCL_VER}.")

function(get_source_archive url ar_name)
	set(full_ar_name "${CMAKE_CURRENT_LIST_DIR}/${ar_name}")
	if (NOT EXISTS ${ar_name})
		MESSAGE("Downloading from '${url}'.")
		FILE(DOWNLOAD ${url} ${full_ar_name})
	else()
		MESSAGE("Found '${ar_name}'.")
	endif()
endfunction(get_source_archive)

# get source archives
set(LLVM_SRC_AR "${CMAKE_CURRENT_LIST_DIR}/llvm-${LLVM_VER}.src.tar.xz")
if (NOT EXISTS ${LLVM_SRC_AR})
	set(LLVM_URL "http://llvm.org/releases/${LLVM_VER}/llvm-${LLVM_VER}.src.tar.xz")
	MESSAGE("Downloading '${LLVM_URL}'..")
	file(DOWNLOAD ${LLVM_URL} ${LLVM_SRC_AR})
else()
	MESSAGE("Found '${LLVM_SRC_AR}'.")
endif()

set(CFE_SRC_AR "${CMAKE_CURRENT_LIST_DIR}/cfe-${LLVM_VER}.src.tar.xz")
if (NOT EXISTS ${CFE_SRC_AR})
	set(CFE_URL "http://llvm.org/releases/${LLVM_VER}/cfe-${LLVM_VER}.src.tar.xz")
	MESSAGE("Downloading '${CFE_URL}'..")
	file(DOWNLOAD ${CFE_URL} ${CFE_SRC_AR})
else()
	MESSAGE("Found '${CFE_SRC_AR}'.")
endif()

set(POCL_SRC_AR "${CMAKE_CURRENT_LIST_DIR}/pocl-0.13.tar.gz")
if (NOT EXISTS ${POCL_SRC_AR})
	set(POCL_URL "http://portablecl.org/downloads/pocl-${POCL_VER}.tar.gz")
	MESSAGE("Downloading ${POCL_URL}..")
	file(DOWNLOAD ${POCL_URL} ${POCL_SRC_AR})
else()
	MESSAGE("Found '${POCL_SRC_AR}'.")
endif()

# unpack
set(LLVM_SRC "${CMAKE_CURRENT_LIST_DIR}/llvm-${LLVM_VER}.src")
if (NOT EXISTS ${LLVM_SRC})
	MESSAGE("Unpacking '${LLVM_SRC_AR}'..")
else()
	MESSAGE("Found




set(CFE_SRC "${CMAKE_CURRENT_LIST_DIR}/cfe-${LLVM_VER}.src")
set(POCL_SRC "${CMAKE_CURRENT_LIST_DIR}/pocl-${POCL_VER}")



#file(DOWNLOAD http://llvm.org/releases/3.8.1/cfe-3.8.1.src.tar.xz cfe.tar.xz)
