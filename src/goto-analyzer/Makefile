SRC = goto_analyzer_main.cpp goto_analyzer_parse_options.cpp \
      taint_parser.cpp taint_analysis.cpp static_analyzer.cpp \
      unreachable_instructions.cpp

OBJ += ../ansi-c/ansi-c$(LIBEXT) \
      ../cpp/cpp$(LIBEXT) \
      ../linking/linking$(LIBEXT) \
      ../big-int/big-int$(LIBEXT) \
      ../goto-programs/goto-programs$(LIBEXT) \
      ../analyses/analyses$(LIBEXT) \
      ../pointer-analysis/pointer-analysis$(LIBEXT) \
      ../langapi/langapi$(LIBEXT) \
      ../json/json$(LIBEXT) \
      ../assembler/assembler$(LIBEXT) \
      ../util/util$(LIBEXT)

INCLUDES= -I ..

LIBS =

include ../config.inc
include ../common

CLEANFILES = goto-analyzer$(EXEEXT)

all: goto-analyzer$(EXEEXT)

ifneq ($(wildcard ../java_bytecode/Makefile),)
  OBJ += ../java_bytecode/java_bytecode$(LIBEXT)
  CP_CXXFLAGS += -DHAVE_JAVA_BYTECODE
  ifneq ($(wildcard $(LIBZIPINC)),)
    LIBS += $(LIBZIPLIB)
  endif
endif

ifneq ($(wildcard ../jsil/Makefile),)
  OBJ += ../jsil/jsil$(LIBEXT)
  CP_CXXFLAGS += -DHAVE_JSIL
endif

ifneq ($(wildcard ../specc/Makefile),)
  OBJ += ../specc/specc$(LIBEXT)
  CP_CXXFLAGS += -DHAVE_SPECC
endif

ifneq ($(wildcard ../php/Makefile),)
  OBJ += ../php/php$(LIBEXT)
  CP_CXXFLAGS += -DHAVE_PHP
endif

###############################################################################

goto-analyzer$(EXEEXT): $(OBJ)
	$(LINKBIN)

.PHONY: goto-analyzer-mac-signed

goto-analyzer-mac-signed: goto-analyzer$(EXEEXT)
	strip goto-analyzer$(EXEEXT) ; codesign -v -s $(OSX_IDENTITY) goto-analyzer$(EXEEXT)
