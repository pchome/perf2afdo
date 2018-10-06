# perf2afdo
Parts from google/autofdo and google/perf_data_converter:quipper

See https://github.com/google/autofdo and https://github.com/google/perf_data_converter/tree/master/src/quipper

**WIP!** For use in Gentoo

Original sources mostly unchanged, dependencies pressent in Gentoo portage tree skipped, tests skipped
`quipper` state : fdc658410dfa9d01b906b115e6fef35c308e55e1
`autofdo` state : db9ca300dd8fa367136fe4a34cc10b8668ded256

The only patch currently used will be applied by ebuild
```patch
--- a/sample_reader.cc
+++ b/sample_reader.cc
@@ -212,7 +212,7 @@
   // focus_binary_re_ is used to match the binary name with the samples.
   for (const auto &event : parser.parsed_events()) {
     if (!event.event_ptr ||
-        event.event_ptr->header().type() != PERF_RECORD_SAMPLE) {
+        event.event_ptr->header().type() != quipper::perf_event_type::PERF_RECORD_SAMPLE) {
       continue;
     }
     if (MatchBinary(event.dso_and_offset.dso_name(), focus_binary)) {
```
