bin_cfg = configuration_data()

bin_cfg.set('uselbr', get_option('use_lbr')?'true':'false')
bin_cfg.set('pebs',   get_option('use_pebs'))

wrappers = [
  'perf2afdo-create',
  'perf2afdo-dump',
  'perf2afdo-record',
  'perf2afdo-diff',
  'perf2afdo-merge',
  'perf2afdo-sample-merge',
  'perf2afdo-update',
]

foreach wrp : wrappers
  configure_file(
    configuration : bin_cfg,
    input         : wrp + '.in',
    output        : wrp,
    install_dir   : get_option('bindir'))
endforeach


# LLVM
if get_option('enable_llvm')
  configure_file(
    configuration : bin_cfg,
    input         : 'perf2afdo-llvm-create.in',
    output        : 'perf2afdo-llvm-create',
    install_dir   : get_option('bindir'))
endif
