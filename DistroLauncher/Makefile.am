bin_PROGRAMS = DistroLauncher

messages.rc: messages.mc
	$(MC) $<

messages.h: messages.rc

# Hacky: no winres.h available with mingw, force include of winresrc.h
# to get the LANG_* and SUBLANG_* defines.
winres.h:
	echo "#include <winresrc.h>" > winres.h

DistroLauncher-res.$(OBJEXT): DistroLauncher.rc \
							   messages.rc \
							   distro.rc \
							   resource.h \
							   winres.h
	$(RC) -D _UNICODE -D UNICODE -l "0x0409" -I $(DISTRO_ID) \
		  --input-format rc -i DistroLauncher.rc \
		  --output-format coff -o $@

DistroLauncher_OBJECTS: messages.h

DistroLauncher_SOURCES = messages.h \
						 BaseLinuxDistroLauncher.cpp \
						 BaseLinuxDistroLauncher.hpp \
						 config.h \
						 DistroLauncher.cpp \
						 Helpers.cpp \
						 helpers.hpp \
						 MyLinuxDistroLauncher.cpp \
						 MyLinuxDistroLauncher.hpp \
						 resource.h \
						 stdafx.cpp \
						 stdafx.h \
						 targetver.h \
						 WslApiLoader.cpp \
						 WslApiLoader.h \
						 DistroLauncher.rc

DistroLauncher_CPPFLAGS = -DMINGW_HAS_SECURE_API -municode -mwindows -m64
DistroLauncher_LDFLAGS = -municode -mwindows -m64 -static
DistroLauncher_LDADD = DistroLauncher-res.$(OBJEXT)
