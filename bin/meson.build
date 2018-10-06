bin_cfg = configuration_data()
bin_cfg.set('uselbr', get_option('use_lbr')?'true':'false')

wrappers = [
  'perf2afdo-create',
  'perf2afdo-dump',
  'perf2afdo-llvm-create',
]

foreach wrp : wrappers
configure_file(
  configuration : bin_cfg,
  input         : wrp + '.in',
  output        : wrp,
  install_dir   : get_option('bindir'))
endforeach
