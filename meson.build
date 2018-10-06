project('autofdo', ['cpp'], default_options: ['cpp_std=c++11', 'unity=on'])

# Smaller binaries with 'unity=on' meson option
#add_project_arguments('-fwhole-program', language : 'cpp')

cc = meson.get_compiler('cpp')

lib_elf      = cc.find_library('elf')
lib_gflags   = cc.find_library('gflags')
lib_glog     = cc.find_library('glog')
lib_protobuf = cc.find_library('protobuf')
lib_openssl  = cc.find_library('crypto')

# Collect data for config.h
cdata = configuration_data()

# Check LLVM
if get_option('enable_llvm')
  find_program('llvm-config')
  cdata.set('HAVE_LLVM', 1)
  cdata.set('CREATE_LLVM_PROF',1)
endif


# Create config.h
configure_file(output : 'config.h', configuration : cdata)


# List/generate sources
protoc = find_program('protoc')

common_src = files([
  'addr2line.cc',
  'gcov.cc',
  'instruction_map.cc',
  'module_grouper.cc',
  'profile_creator.cc',
  'profile_writer.cc',
  'sample_reader.cc',
  'source_info.cc',
  'symbol_map.cc',
  'profile.cc',
])

autofdo_include_path = include_directories('.')

subdir('symbolize')

subdir('third_party/perf_data_converter/src/quipper')


# parts for create_gcov binary
create_gcov_src = [
  common_src,
  symbolize_src,
  'create_gcov.cc',
  quipper_src,
]

executable('create_gcov', create_gcov_src,
  dependencies : [
    lib_openssl,   lib_glog, lib_gflags,
#    symbolize_dep,
    lib_elf,  lib_protobuf
  ],
  install : true)


# parts for dump_gcov binary
dump_gcov_src = [
  common_src,
  symbolize_src,
  'profile_reader.cc',
  'dump_gcov.cc',
  quipper_src,
]

executable('dump_gcov', dump_gcov_src,
  dependencies : [
    lib_openssl,   lib_glog, lib_gflags,
#    symbolize_dep,
    lib_elf,  lib_protobuf
  ],
  install : true)
