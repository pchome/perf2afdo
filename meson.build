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
  llvm_dep = dependency('llvm', version : '>= 5.0',
    modules: [ 'profiledata' ]
  )
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

common_deps = [
  lib_openssl, lib_glog, lib_gflags, lib_elf,  lib_protobuf,
  get_option('enable_llvm') ? llvm_dep : []
]

autofdo_include_path = include_directories('.')

subdir('symbolize')
subdir('third_party/perf_data_converter/src/quipper')


# extend common sources
common_src = [ common_src, symbolize_src, quipper_src ]


# create binaries
foreach m : [ 'create_gcov', 'sample_merger' ]
  executable(m, common_src, m+'.cc', dependencies : common_deps, install : true)
endforeach

foreach m : [ 'dump_gcov', 'profile_diff', 'profile_merger', 'profile_update' ]
  executable(m, common_src, 'profile_reader.cc', m+'.cc', dependencies : common_deps, install : true)
endforeach

if get_option('enable_llvm')
  executable('create_llvm_prof', common_src, 'llvm_profile_writer.cc', 'create_llvm_prof.cc',
    dependencies : common_deps,
    install : true)
endif


# wrappers
subdir('bin')
