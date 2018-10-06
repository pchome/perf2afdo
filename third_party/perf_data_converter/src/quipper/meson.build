perf_data = generator(protoc,
  output    : [ '@BASENAME@.pb.h', '@BASENAME@.pb.cc' ],
  arguments : [ '--cpp_out=@BUILD_DIR@', '-I@CURRENT_SOURCE_DIR@', '@PLAINNAME@' ]
)

# protobuf files for `protoc`
proto = files([
  'perf_data.proto',
  'perf_stat.proto',
])

quipper_src = files([
  'address_mapper.cc',
  'binary_data_utils.cc',
  'buffer_reader.cc',
  'buffer_writer.cc',
  'conversion_utils.cc',
  'data_reader.cc',
  'data_writer.cc',
  'perf_parser.cc',
  'dso.cc',
  'file_reader.cc',
  'file_utils.cc',
  'huge_page_deducer.cc',
#  'perf_converter.cc',
  'perf_data_utils.cc',
  'perf_option_parser.cc',
  'perf_parser.cc',
  'perf_protobuf_io.cc',
  'perf_reader.cc',
#  'perf_recorder.cc',
  'perf_serializer.cc',
  'sample_info_reader.cc',

])

# Add generated `perf_data.pb.{cc,h}` and `perf_stat.pb.{cc,h}`
quipper_src = [
  quipper_src,
  perf_data.process(proto)
]
