AC_INIT([Hqdn3d], [1], [https://github.com/Hinterwaeldlers/vapoursynth-hqdn3d/issues], [Hqdn3d], [https://github.com/Hinterwaeldlers/vapoursynth-hqdn3d/])

: ${CXXFLAGS=""}

AM_INIT_AUTOMAKE([foreign no-dist-gzip dist-xz subdir-objects no-define])
AM_SILENT_RULES([yes])

LT_INIT([disable-static win32-dll])

AC_PROG_CXX

AC_CANONICAL_HOST


X86="false"
ARM="false"

AS_CASE(
  [$host_cpu],
  [i?86],     [BITS="32" X86="true"],
  [x86_64],   [BITS="64" X86="true"],
  [arm*],     [ARM="true"]
)

AS_CASE(
   [$host_os],
   [cygwin*|mingw*],
   [
      AS_IF(
         [test "x$BITS" = "x32"],
         [
          AC_SUBST([PLUGINLDFLAGS], ["-Wl,--kill-at"])
          AC_SUBST([STACKREALIGN], ["-mstackrealign"])
         ]
      )
   ]
)

AS_IF(
      [test "x$X86" = "xtrue"],
      [
       AC_DEFINE([DEGRAINMEDIAN_X86])

       AC_SUBST([MFLAGS], ["-mfpmath=sse -msse2"])
      ]
)

AS_IF(
      [test "x$ARM" = "xtrue"],
      [AC_DEFINE([DEGRAINMEDIAN_ARM])]
)


AM_CONDITIONAL([DEGRAINMEDIAN_X86], [test "x$X86" = "xtrue"])
AM_CONDITIONAL([DEGRAINMEDIAN_ARM], [test "x$ARM" = "xtrue"])


PKG_CHECK_MODULES([VapourSynth], [vapoursynth])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT