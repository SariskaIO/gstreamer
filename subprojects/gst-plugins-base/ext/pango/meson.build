pango_sources = [
  'gstpangoelement.c',
  'gstpangoplugin.c',
  'gstbasetextoverlay.c',
  'gstclockoverlay.c',
  'gsttextoverlay.c',
  'gsttextrender.c',
  'gsttimeoverlay.c',
]

pango_headers = [
  'gsttextrender.h',
  'gsttimeoverlay.h',
  'gsttextoverlay.h',
  'gstbasetextoverlay.h',
  'gstpangoelements.h',
  'gstclockoverlay.h',
]

doc_sources = []
foreach s: pango_sources + pango_headers
  doc_sources += meson.current_source_dir() / s
endforeach

plugin_sources += {
  'pango': pathsep.join(doc_sources)
}

pango_dep = dependency('pangocairo', version : '>=1.22.0', required : get_option('pango'),
  fallback: ['pango', 'libpangocairo_dep'],
  default_options: ['cairo=enabled'])

if pango_dep.found()
  gstpango = library('gstpango',
    pango_sources,
    c_args : gst_plugins_base_args,
    link_args : noseh_link_args,
    include_directories: [configinc, libsinc],
    dependencies : [pango_dep, video_dep, gst_dep, gst_base_dep, libm],
    install : true,
    install_dir : plugins_install_dir,
  )
  plugins += [gstpango]
endif
