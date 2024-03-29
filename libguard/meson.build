# SPDX-License-Identifier: Apache-2.0
headers_include =[
  'include/guard_record.hpp'
]

headers_libguard = [
  'guard_interface.hpp',
  'guard_file.hpp',
  'guard_entity.hpp',
  'guard_log.hpp',
  'guard_common.hpp',
  'guard_exception.hpp',
]

headers = [
  headers_include,
  headers_libguard
]

sources = [
  'guard_interface.cpp',
  'guard_file.cpp',
  'guard_log.cpp',
  'guard_entity.cpp'
]

libguard_headers = ['.', '..']

if get_option('devtree').enabled()
    libpdbg = meson.get_compiler('c').find_library('libpdbg')
    libdtapi = dependency('libdt-api')
    sources += 'devtree/phal_devtree.cpp'
    libguard_headers += include_directories('devtree')
    devtree_deps = [ libpdbg, libdtapi ]
endif

install_headers(
  headers_libguard,
  subdir: 'libguard')

install_headers(
  headers_include,
  subdir: 'libguard/include')

libguard = library(
  'guard',
  sources,
  implicit_include_directories: false,
  include_directories: libguard_headers,
  version: meson.project_version(),
  install: true,
  dependencies : get_option('devtree').enabled() ? devtree_deps : [] )
