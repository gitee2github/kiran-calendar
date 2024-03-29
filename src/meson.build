glib_dep = dependency('glib-2.0')
gobject_dep = dependency('gobject-2.0')
gtk_dep = dependency('gtk+-3.0')
lundate_dep = dependency('lunar-date-3.0')

if get_option('kiran_desktop')
  panelapplet_dep = dependency('libkiranpanelapplet-4.0')
else
  panelapplet_dep = dependency('libmatepanelapplet-4.0')
endif

# Configure data
conf = configuration_data()

conf.set_quoted('VERSION', meson.project_version())
conf.set_quoted('PACKAGE_NAME', meson.project_name())
conf.set_quoted('PACKAGE_VERSION', meson.project_version())
conf.set_quoted('GETTEXT_PACKAGE', meson.project_name())
conf.set_quoted('KIRAN_CALENDAR_DATE_LOCALEDIR', join_paths(get_option('prefix'), get_option('localedir')))
conf.set_quoted('DATADIR', join_paths(get_option('prefix'), get_option('datadir')))
conf.set_quoted('LIBDIR', join_paths(get_option('prefix'), get_option('libdir')))
conf.set_quoted('BINDIR', join_paths(get_option('prefix'), get_option('bindir')))
conf.set_quoted('SYSCONFDIR', join_paths(get_option('prefix'), get_option('sysconfdir')))
conf.set_quoted('LOCALSTATEDIR', join_paths(get_option('prefix'), get_option('localstatedir')))
conf.set_quoted('LIBEXECDIR', join_paths(get_option('prefix'), get_option('libexecdir')))

configure_file(
  output : 'config.h',
  configuration : conf
  )

time_date_ch = custom_target (
  'gen-code-time-date',
  input : '../data/com.kylinsec.Kiran.SystemDaemon.TimeDate.xml',
  output : ['kiran-time-date-gen.h', 'kiran-time-date-gen.c'],
  command : [find_program('gdbus-codegen'),
             '--c-namespace', 'Kiran',
             '--interface-prefix', 'com.kylinsec.Kiran.SystemDaemon',
             '--generate-c-code', 'kiran-time-date-gen',
             '--output-directory', 'src/',
             '@INPUT@'],
  build_by_default: true
)


executable('kiran-calendar-test',
  'kiran-calendar-test.c',
  'kiran-calendar.c',
  'common.c',
  install : false,
  c_args: '-g',
  dependencies : [glib_dep, gobject_dep, gtk_dep, lundate_dep]
)

executable('kiran-clock-test',
  'kiran-clock-test.c',
  'kiran-calendar.c',
  'kiran-clock.c',
  'kiran-calendar-window.c',
  'common.c',
  time_date_ch[1],
  install : false,
  c_args: '-g',
  dependencies : [glib_dep, gobject_dep, gtk_dep, lundate_dep]
)

executable('kiran-clock-applet',
  'kiran-clock-applet.c',
  'kiran-calendar.c',
  'kiran-clock.c',
  'kiran-calendar-window.c',
  'common.c',
  time_date_ch[1],
  install : true,
  install_dir: libexecdir,
  dependencies : [glib_dep, gobject_dep, gtk_dep, lundate_dep, panelapplet_dep]
)
