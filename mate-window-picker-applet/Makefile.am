appletlibdir = $(libdir)/mate-panel
appletlib_LTLIBRARIES = libmate-window-picker-applet.la

PKGDATADIR = $(datadir)/mate-window-picker-applet
AM_CFLAGS=\
	$(MATEWINDOWPICKER_DEPS_CFLAGS) \
	$(GCC_FLAGS) \
	-I$(top_builddir) \
	-I$(top_srcdir) \
	-D_GNU_SOURCE \
	-DMATELOCALEDIR=\""$(datadir)/locale"\" \
	-DPKGDATADIR=\"$(PKGDATADIR)\" \
	-DMATEWINDOWPICKER_MENU_UI_DIR=\""$(xmluidir)"\" \
	-DENABLE_IN_PROCESS \
	-DPANEL_APPLET_FACTORY=MATE_PANEL_APPLET_IN_PROCESS_FACTORY \
	$(WARN_CFLAGS)

libmate_window_picker_applet_la_LIBADD = \
	$(MATEWINDOWPICKER_DEPS_LIBS) \
	-lm

libmate_window_picker_applet_la_LDFLAGS = \
	-export-dynamic \
	-module \
	-avoid-version \
	-shared

libmate_window_picker_applet_la_SOURCES = \
	applet.c \
	task-item.c \
	task-item.h \
	task-list.c \
	task-list.h \
	task-title.c \
	task-title.h 

appletdir       = $(datadir)/mate-panel/applets
applet_in_files = org.mate.panel.MateWindowPicker.mate-panel-applet.desktop.in
applet_DATA     = $(applet_in_files:.mate-panel-applet.desktop.in=.mate-panel-applet)

$(applet_in_files): $(applet_in_files).in Makefile
	$(AM_V_GEN)sed \
	-e "s|\@LOCATION\@|$(APPLET_LOCATION)|" \
	$< > $@

$(applet_DATA): $(applet_in_files) Makefile
	$(AM_V_GEN) $(MSGFMT) --desktop --keyword=Name --keyword=Description --template $< -d $(top_srcdir)/po -o $@

APPLET_LOCATION=$(libdir)/mate-panel/libmate-window-picker-applet.so

gsettingsschema_in_files = org.mate.panel.applet.mate-window-picker-applet.gschema.xml.in

gsettings_SCHEMAS = $(gsettingsschema_in_files:.xml.in=.xml)
@GSETTINGS_RULES@

xmluidir = $(datadir)/mate-panel/ui
xmlui_DATA = mate-window-picker-applet-menu.xml

EXTRA_DIST = \
	$(applet_in_files).in \
	$(ui_DATA) \
	$(convert_DATA) \
	$(gsettingsschema_in_files) \
	$(xmlui_DATA)

CLEANFILES = \
	$(applet_DATA) \
	$(applet_in_files) \
	$(gsettings_SCHEMAS) \
	*.gschema.valid
