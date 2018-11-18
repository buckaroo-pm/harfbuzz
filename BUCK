have_graphite = read_config('harfbuzz', 'have_graphite', False)

graphite_srcs = glob([
  'src/hb-graphite2.cc', 
])

gnu_srcs = glob([
  'src/hb-glib.cc', 
  'src/hb-gobject-*.cc', 
])

macos_srcs = glob([
  'src/hb-coretext.cc', 
])

windows_srcs = glob([
  'src/hb-uniscribe.cc', 
  'src/hb-directwrite.cc', 
])

platform_srcs = graphite_srcs + gnu_srcs + macos_srcs + windows_srcs

macos_preprocessor_flags = [
  '-DTARGET_OS_OSX=1', 
  '-DHAVE_ICU=1', 
  '-DHAVE_UCDN=1', 
  '-DHAVE_CORETEXT=1', 
]

cxx_library(
  name = 'harfbuzz', 
  header_namespace = '', 
  exported_headers = subdir_glob([
    ('src', 'hb*.h'), 
  ], prefix = 'harfbuzz'), 
  headers = subdir_glob([
    ('src/hb-ucdn', '**/*.h'), 
    ('src', '**/*.h'), 
  ]), 
  platform_preprocessor_flags = [
    ('macos.*', macos_preprocessor_flags), 
  ], 
  srcs = glob([
    'src/hb-ucdn/**/*.cc', 
    'src/**/hb-*.cc', 
  ], exclude = glob([
    'src/**/hb*shape*.cc', 
  ]) + platform_srcs), 
  platform_srcs = [
    ('macos.*', macos_srcs), 
    ('windows.*', windows_srcs), 
  ], 
  deps = [
    'buckaroo.github.buckaroo-pm.icu4c//:icu4c', 
    'buckaroo.github.buckaroo-pm.luadist-freetype//:freetype', 
  ], 
  visibility = [
    'PUBLIC', 
  ], 
)
