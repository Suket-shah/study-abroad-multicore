###############################################################################
# SPECtools95 
#   Version 0.2
#   This makefile should NOT be changed other than to customize for a 
#   particular benchmark.  Users may overide variables by placing them
#   in the Makefile.spec file.  Or by using the "runspec" program to 
#   build the Makefile.spec file for them.

###############################################################################
#	BENCHMARK	-- standard definitions for this benchmark

NUMBER    = 126
NAME      = gcc
EXEBASE   = cc1
OFILES    = c-parse c-lang c-lex c-pragma c-decl c-typeck c-convert c-aux-info c-common c-iterate bc-emit bc-optab toplev version tree print-tree stor-layout fold-const function stmt expr calls expmed explow optabs varasm rtl print-rtl rtlanal emit-rtl real dbxout sdbout dwarfout xcoffout integrate jump cse loop unroll flow stupid combine regclass local-alloc global reload reload1 caller-save insn-peep reorg sched final recog reg-stack insn-opinit insn-recog insn-extract insn-output insn-emit insn-attrtab aux-output getpwd convert ucbqsort obstack ${EXTRA_OBJS}
LIBS      = 
LD        = $(CC) $(CFLAGS)


###############################################################################
#	DEFINES		-- standard definitions for SPEC
#                          these may be overriden in Makefile.spec
BENCHMARK = $(NUMBER).$(NAME)
EXT       = 
OBJS      = $(addsuffix $(OBJ),$(OFILES))
CC        = cc
CFLAGS    = $(EXTRA_CFLAGS) -DSPEC $(FDO_FLAGS) $(OPTIMIZE)
FC        = f77
FFLAGS    = $(EXTRA_FFLAGS) $(FDO_FLAGS) $(OPTIMIZE)
LDFLAGS   = $(EXTRA_LDFLAGS) $(FDO_LDFLAGS)
LDOPT     = -o $@
OPTIMIZE  = $(EXTRA_OPTIMIZE) -O
OBJOPT    = -c -o $@
OBJ       = .o
SPECSHELL = /bin/sh
ECHO      = echo
PATHSEP   = /
PARENTDIR = ..
BINDIR    = $(PARENTDIR)$(PATHSEP)exe$(TUNE)
EXENAME   = $(EXEBASE)$(EXT)
BINARY    = $(BINDIR)$(PATHSEP)$(EXENAME)

ifeq ($(FDO),pass1)
        FDO_FLAGS=$(PASS1) $(PASS1_CFLAGS)
	FDO_LDFLAGS=$(PASS1_LDFLAGS)
endif
ifeq ($(FDO),pass2)
        FDO_FLAGS=$(PASS2) $(PASS2_CFLAGS)
	FDO_LDFLAGS=$(PASS2_LDFLAGS)
endif


###############################################################################
#	VENDOR		-- where we include any vendor specific information
ifneq ($(NOINC),yes)
	include Makefile.spec
endif


###############################################################################
#	TARGETS		-- Rules to build benchmark executables
error: 
	@$(ECHO) "This makefile is only used for building binaries now"
	@$(ECHO) "to run the SPEC suite please use 'runspec'"
	@$(ECHO)

build: $(EXTRA_TARGETS) $(BINARY)

.SUFFIXES: $(OBJ)
.c$(OBJ):
	$(CC) $(OBJOPT) $(CFLAGS) $<

# template build target, should work for simple builds
$(BINARY): $(OBJS)
	$(LD) $(LDFLAGS) $(LDOPT) $(OBJS) $(LIBS) $(EXTRA_LIBS)

# to clean things up
.PHONY: clean clobber
clean:
ifeq ($(OBJ),.c)
	rm -rf core *.err *.out
else
	rm -rf $(OBJS) core *.err *.out
endif

clobber: clean
	rm -rf $(BINARY)
