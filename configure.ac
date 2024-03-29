AC_INIT([gtksourceviewmm], [3.91.1],
        [http://bugzilla.gnome.org/enter_bug.cgi?product=gtksourceviewmm],
        [gtksourceviewmm], [http://projects.gnome.org/gtksourceviewmm/])
AC_PREREQ([2.62])

AC_CONFIG_SRCDIR([gtksourceview/gtksourceviewmm.h])
AC_CONFIG_AUX_DIR([build])
AC_CONFIG_MACRO_DIR([build])
AC_CONFIG_HEADERS([build/config.h gtksourceview/gtksourceviewmmconfig.h])

AM_INIT_AUTOMAKE([1.9 -Wno-portability check-news dist-bzip2 no-define nostdinc tar-ustar])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES([yes])])
AM_MAINTAINER_MODE
AC_ARG_VAR([ACLOCAL_FLAGS], [aclocal flags, e.g. -I <macro dir>])

MM_PREREQ([0.9.8])
MM_INIT_MODULE([gtksourceviewmm-4.0])

# Copy the mm-common .pl scripts into docs/,
# and use them from there,
# so we can dist them to avoid a tarball-build dependency.
MM_CONFIG_DOCTOOL_DIR([docs])

AC_SUBST([GTKSOURCEVIEWMM_SO_VERSION], [0:0:0])

LT_INIT([win32-dll disable-static])
AC_PROG_CXX
MM_AX_CXX_COMPILE_STDCXX_11([noext],[mandatory])

AC_SUBST([GTKSOURCEVIEWMM_MODULES], ['glibmm-2.4 >= 2.46.1 gtkmm-3.0 >= 3.18.0 gtksourceview-4 >= 3.99.0'])
PKG_CHECK_MODULES([GTKSOURCEVIEWMM], [$GTKSOURCEVIEWMM_MODULES])

MM_PKG_CONFIG_SUBST([GTHREAD_CFLAGS], [--cflags-only-other gthread-2.0])
MM_PKG_CONFIG_SUBST([GMMPROC_DIR], [--variable=gmmprocdir glibmm-2.4])
MM_PKG_CONFIG_SUBST([GMMPROC_EXTRA_M4_DIR], [--variable=gmmprocm4dir pangomm-1.4 atkmm-1.6 gtkmm-3.0])

MM_ARG_DISABLE_DEPRECATED_API([GTKSOURCEVIEWMM])

MM_ARG_ENABLE_DOCUMENTATION
MM_ARG_WITH_TAGFILE_DOC([libstdc++.tag], [mm-common-libstdc++])
MM_ARG_WITH_TAGFILE_DOC([libsigc++-2.0.tag], [sigc++-2.0])
MM_ARG_WITH_TAGFILE_DOC([glibmm-2.4.tag], [glibmm-2.4])
MM_ARG_WITH_TAGFILE_DOC([cairomm-1.0.tag], [cairomm-1.0])
MM_ARG_WITH_TAGFILE_DOC([pangomm-1.4.tag], [pangomm-1.4])
MM_ARG_WITH_TAGFILE_DOC([gtkmm-3.0.tag], [gtkmm-3.0])

AC_LANG([C++])

# Re-enable disabling of PANGO API when gtksourceview and gtk+ stop using deprecated API (PangoDirection) in their API.
MM_ARG_ENABLE_WARNINGS([GTKSOURCEVIEWMM_WXXFLAGS],
                       [-Wall -Wno-long-long],
                       [-pedantic -Wall -Wextra -Wno-long-long],
                       [G ATK GDK GDK_PIXBUF GTK GTKSOURCEVIEW GLIBMM PANGOMM ATKMM GDKMM GTKMM])

AC_CONFIG_FILES([Makefile
                 codegen/Makefile
                 gtksourceview/${GTKSOURCEVIEWMM_MODULE_NAME}.pc:gtksourceview/gtksourceviewmm.pc.in
                 gtksourceview/${GTKSOURCEVIEWMM_MODULE_NAME}-uninstalled.pc:gtksourceview/gtksourceviewmm-uninstalled.pc.in
                 gtksourceview/src/Makefile
                 gtksourceview/gtksourceviewmm/Makefile
                 tests/Makefile
                 docs/Makefile
                 docs/reference/Doxyfile])

AC_OUTPUT
