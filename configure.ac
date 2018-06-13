# This is the autoconf script for the sample dispatch library, which
# allows netCDF to read files of a user-defined format. In the case of
# this sample project, HDF4 is the format. There is no need for this
# library to be used operationally, as netCDF already includes the
# capability to read HDF4. This is a sample of how to create a
# dispatch library for netCDF's user-defined format feature.
#
# Ed Hartnett 6/2/18

# Set up autoconf.
AC_PREREQ([2.69])
AC_INIT([sample-netcdf-disapatch], [1.0.0], [edward.hartnett@noaa.gov])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIRS([m4])

# Set up automake.
AM_INIT_AUTOMAKE([foreign subdir-objects])

# Set up libtool.
LT_PREREQ([2.2])
LT_INIT()

# Checks for programs.
AC_PROG_CC

# Set these to get correct results from netCDF header files.
AC_DEFINE([USE_HDF4], 1, [Set for netCDF headers.])
AC_DEFINE([USE_NETCDF4], 1, [Set for netCDF headers.])

# Does the user want to enable netcdf-4 logging?
AC_MSG_CHECKING([whether logging is enabled])
AC_ARG_ENABLE([logging],
              [AS_HELP_STRING([--enable-logging],
                              [Enable logging capability - for developers only  .])])
test "x$enable_logging" = xyes || enable_logging=no
AC_MSG_RESULT([$enable_logging])
if test "x$enable_logging" = xyes; then
   AC_DEFINE([AB_LOGGING], 1, [If true, turn on AB logging.])
   AC_DEFINE([LOGGING], 1, [If true, turn on netCDF logging.])
fi

# Does the user want to run tests? Tests are turned off by default so
# that a combined build package can include the dispatch library and
# netCDF. The dispatch library is built first, so cannot run tests
# that require the netCDF library.
AC_MSG_CHECKING([whether tests are enabled])
AC_ARG_ENABLE([tests],
              [AS_HELP_STRING([--enable-tests],
                              [Run tests with make check.])])
test "x$enable_tests" = xyes || enable_tests=no
AC_MSG_RESULT([$enable_tests])
AM_CONDITIONAL(ENABLE_TESTS,[test x$enable_tests = xyes])

# Checks for libraries.
AC_CHECK_LIB(netcdf, nc_def_user_format)
if test x${ac_cv_lib_netcdf_nc_def_user_format} != xyes; then
   AC_MSG_ERROR([Must have netcdf])
fi

# Checks for header files.
AC_CHECK_HEADERS([stddef.h stdlib.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T

# Checks for library functions.
#AC_FUNC_MALLOC
#AC_CHECK_FUNCS([strdup])

AC_CONFIG_FILES([Makefile
                 include/Makefile
                 test/Makefile
                 src/Makefile])
AC_OUTPUT
