thisdir = class/Microsoft.Build.Engine
SUBDIRS = 
include ../../build/rules.make

XBUILD_DIR=$(topdir)/tools/xbuild
include $(XBUILD_DIR)/xbuild.make

LIBRARY = Microsoft.Build.Engine.dll

LIB_REFS = System System.Core System.Xml
LIB_MCS_FLAGS = \
	/r:$(corlib)		\
	/r:System.dll		\
	/r:System.Core.dll	\
	/r:System.Xml.dll	\
	/r:$(XBUILD_FRAMEWORK)	\
	/r:$(XBUILD_UTILITIES)

TEST_MCS_FLAGS = \
	/r:$(XBUILD_FRAMEWORK)	\
	/r:$(XBUILD_UTILITIES) \
	/r:System.Xml.dll

EXTRA_DISTFILES = \
	Test/resources/TestTasks.cs		\
	Test/resources/*.*proj	\
	Test/resources/*.csproj

Test/resources/TestTasks-$(PROFILE).dll: Test/resources/TestTasks.cs
	$(CSCOMPILE) /out:$@ Test/resources/TestTasks.cs /r:$(XBUILD_FRAMEWORK) /r:$(XBUILD_UTILITIES) /target:library

clean-test-resources:
	rm -f Test/resources/TestTasks*.dll Test/resources/TestTasks*.dll.mdb

test-local: compile-resources

compile-resources: Test/resources/TestTasks-$(PROFILE).dll
	cp Test/resources/TestTasks-$(PROFILE).dll Test/resources/TestTasks.dll
	cp Test/resources/TestTasks-$(PROFILE).dll.mdb Test/resources/TestTasks.dll.mdb

clean-local: clean-test-resources

include $(XBUILD_DIR)/xbuild_test.make
include ../../build/library.make
