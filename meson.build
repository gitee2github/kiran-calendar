project ('kiran-calendar', 'c',
  version : '1.22',
  license : 'LGPLv2+',
  meson_version : '>=0.44',
  default_options : [
    'c_std=gnu99',
    'prefix=/usr',
    'sysconfdir=/etc'
  ]
)

compiler = meson.get_compiler('c')
project_name = meson.project_name()
project_version = meson.project_version()

prefix = get_option('prefix')
datadir = join_paths(prefix, get_option('datadir'))
libexecdir = join_paths(prefix, get_option('libexecdir'))
schemadir = join_paths (datadir, 'glib-2.0', 'schemas')

i18n  = import('i18n')

if get_option('kiran_desktop')
  panel_name = 'kiran-panel'
else
  panel_name = 'mate-panel'
endif

subdir('data')
subdir('src')
subdir('po')
