#
# This file is part of John the Ripper password cracker,
# Copyright (c) 1996-2010 by Solar Designer
#
# Modified by Truls Edvard Stokke for BitRipper imageboard
# tripcode cracker.
#
# See LICENSE file for details regarding files originating
# from John the Ripper.
#

CC = gcc
AS = $(CC)
LD = $(CC)
CPP = $(CC)
CP = cp
LN = ln -sf
RM = rm -f
TR = tr
SED = sed
NULL = /dev/null
CPPFLAGS = -E
OMPFLAGS =
# gcc with OpenMP
#OMPFLAGS = -fopenmp
# Sun Studio with OpenMP (set the OMP_NUM_THREADS env var at runtime)
#OMPFLAGS = -xopenmp
CFLAGS = -c -Wall -O2 -fomit-frame-pointer $(OMPFLAGS) -std=c99
ASFLAGS = -c $(OMPFLAGS)
LDFLAGS = -s $(OMPFLAGS)
OPT_NORMAL = -funroll-loops
OPT_INLINE = -finline-functions

BIT_OBJS = bitripper.o DES_std.o DES_bs.o DES_bs_b.o common.o

PROJ = ../bitripper
PROJ_WIN32 = ../bitripper.exe

default:
	@echo "To build BitRipper, type:"
	@echo "	make clean SYSTEM"
	@echo "where SYSTEM can be one of the following:"
	@echo "linux-x86-64             Linux, x86-64 with SSE2 (best)"
#	@echo "linux-x86-64-32-sse2     Linux, x86-64, 32-bit with SSE2"
#	@echo "linux-x86-64-32-mmx      Linux, x86-64, 32-bit with MMX"
	@echo "linux-x86-sse2           Linux, x86 with SSE2 (best if 32-bit)"
	@echo "linux-x86-mmx            Linux, x86 with MMX"
	@echo "linux-x86-any            Linux, x86"
	@echo "linux-alpha              Linux, Alpha"
	@echo "linux-sparc              Linux, SPARC 32-bit"
	@echo "linux-ppc32-altivec      Linux, PowerPC w/AltiVec (best)"
	@echo "linux-ppc32              Linux, PowerPC 32-bit"
#	@echo "linux-ppc64-altivec      Linux, PowerPC 64-bit w/AltiVec"
	@echo "linux-ppc64              Linux, PowerPC 64-bit"
	@echo "linux-ia64               Linux, IA-64"
	@echo "freebsd-x86-64           FreeBSD, x86-64 with SSE2 (best)"
	@echo "freebsd-x86-sse2         FreeBSD, x86 with SSE2 (best if 32-bit)"
	@echo "freebsd-x86-mmx          FreeBSD, x86 with MMX"
	@echo "freebsd-x86-any          FreeBSD, x86"
	@echo "freebsd-alpha            FreeBSD, Alpha"
	@echo "openbsd-x86-64           OpenBSD, x86-64 with SSE2 (best)"
	@echo "openbsd-x86-sse2         OpenBSD, x86 with SSE2 (best if 32-bit)"
	@echo "openbsd-x86-mmx          OpenBSD, x86 with MMX"
	@echo "openbsd-x86-any          OpenBSD, x86"
	@echo "openbsd-alpha            OpenBSD, Alpha"
	@echo "openbsd-sparc64          OpenBSD, SPARC 64-bit (best)"
	@echo "openbsd-sparc            OpenBSD, SPARC 32-bit"
	@echo "openbsd-ppc32            OpenBSD, PowerPC 32-bit"
	@echo "openbsd-ppc64            OpenBSD, PowerPC 64-bit"
	@echo "openbsd-pa-risc          OpenBSD, PA-RISC"
	@echo "openbsd-vax              OpenBSD, VAX"
	@echo "netbsd-sparc64           NetBSD, SPARC 64-bit"
	@echo "netbsd-vax               NetBSD, VAX"
	@echo "solaris-sparc64-cc       Solaris, SPARC V9 64-bit, cc (best)"
	@echo "solaris-sparc64-gcc      Solaris, SPARC V9 64-bit, gcc"
	@echo "solaris-sparcv9-cc       Solaris, SPARC V9 32-bit, cc"
	@echo "solaris-sparcv8-cc       Solaris, SPARC V8 32-bit, cc"
	@echo "solaris-sparc-gcc        Solaris, SPARC 32-bit, gcc"
	@echo "solaris-x86-64-cc        Solaris, x86-64 with SSE2, cc (best)"
	@echo "solaris-x86-64-gcc       Solaris, x86-64 with SSE2, gcc"
	@echo "solaris-x86-sse2-cc      Solaris 9 4/04+, x86 with SSE2, cc"
	@echo "solaris-x86-sse2-gcc     Solaris 9 4/04+, x86 with SSE2, gcc"
	@echo "solaris-x86-mmx-cc       Solaris, x86 with MMX, cc"
	@echo "solaris-x86-mmx-gcc      Solaris, x86 with MMX, gcc"
	@echo "solaris-x86-any-cc       Solaris, x86, cc"
	@echo "solaris-x86-any-gcc      Solaris, x86, gcc"
	@echo "sco-x86-any-gcc          SCO, x86, gcc"
	@echo "sco-x86-any-cc           SCO, x86, cc"
	@echo "tru64-alpha              Tru64 (Digital UNIX, OSF/1), Alpha"
	@echo "aix-ppc32                AIX, PowerPC 32-bit"
	@echo "macosx-x86-64            Mac OS X 10.5+, Xcode 3.0+, x86-64 with SSE2 (best)"
	@echo "macosx-x86-sse2          Mac OS X, x86 with SSE2"
	@echo "macosx-ppc32-altivec     Mac OS X, PowerPC w/AltiVec (best)"
	@echo "macosx-ppc32             Mac OS X, PowerPC 32-bit"
#	@echo "macosx-ppc64-altivec     Mac OS X, PowerPC 64-bit w/AltiVec"
	@echo "macosx-ppc64             Mac OS X 10.4+, PowerPC 64-bit"
	@echo "hpux-pa-risc-gcc         HP-UX, PA-RISC, gcc"
	@echo "hpux-pa-risc-cc          HP-UX, PA-RISC, ANSI cc"
	@echo "irix-mips64-r10k         IRIX, MIPS 64-bit (R10K) (best)"
	@echo "irix-mips64              IRIX, MIPS 64-bit"
	@echo "irix-mips32              IRIX, MIPS 32-bit"
	@echo "win32-cygwin-x86-sse2    Win32, Cygwin, x86 with SSE2 (best)"
	@echo "win32-cygwin-x86-mmx     Win32, Cygwin, x86 with MMX"
	@echo "win32-cygwin-x86-any     Win32, Cygwin, x86"
	@echo "beos-x86-sse2            BeOS, x86 with SSE2 (best)"
	@echo "beos-x86-mmx             BeOS, x86 with MMX"
	@echo "beos-x86-any             BeOS, x86"

linux-x86-64:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86-64.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

linux-x86-64-32-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-sse.o" \
		CFLAGS="$(CFLAGS) -m32 -DHAVE_CRYPT" \
		ASFLAGS="$(ASFLAGS) -m32" \
		LDFLAGS="$(LDFLAGS) -m32 -lcrypt"

linux-x86-64-32-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-mmx.o" \
		CFLAGS="$(CFLAGS) -m32 -DHAVE_CRYPT" \
		ASFLAGS="$(ASFLAGS) -m32" \
		LDFLAGS="$(LDFLAGS) -m32 -lcrypt"

linux-x86-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-sse.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

linux-x86-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-mmx.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

linux-x86-any:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

linux-alpha:
	$(LN) alpha.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  alpha.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

# This target is currently "undocumented" as ccc generates much slower
# code for the large unrolled loops in John; let's hope it gets fixed.
linux-alpha-ccc:
	$(LN) alpha.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  alpha.o" \
		CC=ccc \
		CFLAGS="-c -Wf,-switch,noil_schedule -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt" \
		OPT_NORMAL="-fast" \
		OPT_INLINE="-O2 -arch host"

linux-sparc:
	$(LN) sparc32.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

linux-ppc32-altivec:
	$(LN) ppc32alt.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt" \
		OPT_INLINE="-finline-functions -finline-limit=4000 -maltivec"

linux-ppc32:
	$(LN) ppc32.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

# This is slightly slower than linux-ppc32-altivec for most hash types.
linux-ppc64-altivec:
	$(LN) ppc64alt.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -m64 -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -m64 -lcrypt" \
		OPT_INLINE="-finline-functions -finline-limit=4000 -maltivec"

linux-ppc64:
	$(LN) ppc64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -m64 -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -m64 -lcrypt" \
		OPT_INLINE="-finline-functions -finline-limit=4000"

linux-ia64:
	$(LN) ia64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lcrypt"

freebsd-x86-64:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86-64.o"

freebsd-x86-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-sse.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

freebsd-x86-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-mmx.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

freebsd-x86-any:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

freebsd-x86-any-a.out:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o" \
		ASFLAGS="$(ASFLAGS) -DUNDERSCORES -DALIGN_LOG -DBSD"

freebsd-alpha:
	$(LN) alpha.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) alpha.o"

openbsd-x86-64:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86-64.o"

openbsd-x86-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-sse.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

openbsd-x86-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-mmx.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

openbsd-x86-any:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o" \
		ASFLAGS="$(ASFLAGS) -DBSD"

openbsd-x86-any-a.out:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o" \
		ASFLAGS="$(ASFLAGS) -DUNDERSCORES -DALIGN_LOG -DBSD"

openbsd-alpha:
	$(LN) alpha.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) alpha.o"

openbsd-sparc64:
	$(LN) sparc64.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="$(CFLAGS) -m64 -mcpu=ultrasparc" \
		LDFLAGS="$(LDFLAGS) -m64"

openbsd-sparc:
	$(LN) sparc32.h arch.h
	$(MAKE) $(PROJ)

openbsd-ppc32:
	$(LN) ppc32.h arch.h
	$(MAKE) $(PROJ)

openbsd-ppc64:
	$(LN) ppc64.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="$(CFLAGS) -m64" \
		LDFLAGS="$(LDFLAGS) -m64" \
		OPT_INLINE="-finline-functions -finline-limit=4000"

openbsd-pa-risc:
	$(LN) pa-risc.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="-c -Wall -O3 -fomit-frame-pointer"

openbsd-vax:
	$(LN) vax.h arch.h
	$(MAKE) $(PROJ)

netbsd-sparc64:
	$(LN) sparc64.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="$(CFLAGS) -m64 -mcpu=ultrasparc" \
		LDFLAGS="$(LDFLAGS) -m64"

netbsd-vax:
	$(LN) vax.h arch.h
	$(MAKE) $(PROJ)

solaris-sparc64-cc:
	$(LN) sparc64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CC=cc \
		CFLAGS="-c -fast -xarch=native64 -DHAVE_CRYPT $(OMPFLAGS)" \
		LDFLAGS="-s -xarch=native64 $(OMPFLAGS) -lc -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-sparc64-gcc:
	$(LN) sparc64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -m64 -mcpu=ultrasparc -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -m64 -lrt"

solaris-sparcv9-cc:
	$(LN) sparc32.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CC=cc \
		CFLAGS="-c -xO4 -xarch=v8plusa -xchip=ultra -DHAVE_CRYPT $(OMPFLAGS)" \
		LDFLAGS="-s $(OMPFLAGS) -lc -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-sparcv8-cc:
	$(LN) sparc32.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CC=cc \
		CFLAGS="-c -xO4 -xarch=v8 -DHAVE_CRYPT $(OMPFLAGS)" \
		LDFLAGS="-s $(OMPFLAGS) -lc -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-sparc-gcc:
	$(LN) sparc32.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) " \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lrt"

solaris-x86-64-cc:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86-64.o" \
		CC=cc \
		CFLAGS="-c -fast -xarch=native64 -DHAVE_CRYPT $(OMPFLAGS)" \
		ASFLAGS="-c -xarch=native64 $(OMPFLAGS)" \
		LDFLAGS="-s -xarch=native64 $(OMPFLAGS) -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-x86-64-gcc:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86-64.o" \
		CFLAGS="$(CFLAGS) -m64 -DHAVE_CRYPT" \
		ASFLAGS="$(CFLAGS) -m64" \
		LDFLAGS="$(LDFLAGS) -m64 -lrt"

solaris-x86-sse2-cc:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  solaris-x86.o x86-sse.o" \
		CC=cc \
		CFLAGS="-c -fast -xarch=native -DHAVE_CRYPT $(OMPFLAGS)" \
		ASFLAGS="-c -xarch=native $(OMPFLAGS)" \
		LDFLAGS="-s -xarch=native $(OMPFLAGS) -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-x86-sse2-gcc:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-sse.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lrt"

solaris-x86-mmx-cc:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  solaris-x86.o x86-mmx.o" \
		CC=cc \
		CFLAGS="-c -fast -xarch=native -DHAVE_CRYPT $(OMPFLAGS)" \
		ASFLAGS="-c -xarch=native $(OMPFLAGS)" \
		LDFLAGS="-s -xarch=native $(OMPFLAGS) -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-x86-mmx-gcc:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS)  x86.o x86-mmx.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lrt"

solaris-x86-any-cc:
	$(RM) arch.h
	ln -s x86-any.h arch.h
	$(MAKE) $(PROJ) \
		SHELL=/bin/sh \
		BIT_OBJS="$(BIT_OBJS)  solaris-x86.o" \
		CC=cc \
		CFLAGS="-c -xO4 -DHAVE_CRYPT $(OMPFLAGS)" \
		ASFLAGS="-c $(OMPFLAGS)" \
		LDFLAGS="-s $(OMPFLAGS) -lc -lrt" \
		OPT_NORMAL="" \
		OPT_INLINE="-xinline=s1,s2,s3,s4,s5,s6,s7,s8"

solaris-x86-any-gcc:
	$(RM) arch.h
	ln -s x86-any.h arch.h
	$(MAKE) $(PROJ) \
		SHELL=/bin/sh \
		BIT_OBJS="$(BIT_OBJS)  solaris-x86.o" \
		CFLAGS="$(CFLAGS) -DHAVE_CRYPT" \
		LDFLAGS="$(LDFLAGS) -lc -lrt"

# Older versions of Sun's assembler had a line length restriction (and some
# other problems, which affect newer versions as well and which are worked
# around in x86.S).
solaris-x86.o: x86.S
	$(CPP) $(CPPFLAGS) -P -DDUMBAS x86.S | $(TR) \; \\n > tmp.s
	$(AS) $(ASFLAGS) tmp.s -o solaris-x86.o
	$(RM) tmp.s

sco-x86-any-gcc:
	$(RM) arch.h
	ln -s x86-any.h arch.h
	$(MAKE) $(PROJ) \
		SHELL=/bin/sh \
		BIT_OBJS="$(BIT_OBJS) sco-x86.o"

sco-x86-any-cc:
	$(RM) arch.h
	ln -s x86-any.h arch.h
	$(MAKE) $(PROJ) \
		SHELL=/bin/sh \
		BIT_OBJS="$(BIT_OBJS) sco-x86.o" \
		CC=cc \
		CFLAGS="-c -b elf -O3" \
		ASFLAGS="-c -b elf" \
		OPT_NORMAL="-K loop_unroll,no_inline" \
		OPT_INLINE="-K inline"

# SCO is even worse than Solaris x86
sco-x86.o: x86.S
	$(CPP) $(CPPFLAGS) -DDUMBAS x86.S | \
		$(TR) \; \\n | $(SED) 's/\([%.]\) /\1/g' > tmp.s
	$(AS) $(ASFLAGS) tmp.s -o sco-x86.o
	$(RM) tmp.s

tru64-alpha:
	$(LN) alpha.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) digipaq-alpha.o" \
		CC=cc \
		CFLAGS="-c -O4 -arch host" \
		OPT_NORMAL="" \
		OPT_INLINE="-inline all"

# Digital/Compaq's cc and make use the .S suffix for a different purpose...
digipaq-alpha.o: alpha.S
	$(CPP) $(CPPFLAGS) alpha.S > tmp.s
	$(AS) $(ASFLAGS) tmp.s -o digipaq-alpha.o
	$(RM) tmp.s

aix-ppc32:
	$(LN) ppc32.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -qunroll=2 -qarch=ppc -qchars=signed" \
		LDFLAGS="-s -lbsd" \
		OPT_NORMAL="-O2" \
		OPT_INLINE="-O3 -Q=99 -w"

macosx-x86-64:
	$(LN) x86-64.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86-64.o" \
		ASFLAGS="$(ASFLAGS) -m64 -DUNDERSCORES -DBSD -DALIGN_LOG" \
		CFLAGS="$(CFLAGS) -m64" \
		LDFLAGS="$(LDFLAGS) -m64"

macosx-x86-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-sse.o" \
		ASFLAGS="$(ASFLAGS) -m32 -DUNDERSCORES -DBSD -DALIGN_LOG" \
		CFLAGS="$(CFLAGS) -m32" \
		LDFLAGS="$(LDFLAGS) -m32"

macosx-x86-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-mmx.o" \
		ASFLAGS="$(ASFLAGS) -m32 -DUNDERSCORES -DBSD -DALIGN_LOG" \
		CFLAGS="$(CFLAGS) -m32" \
		LDFLAGS="$(LDFLAGS) -m32"

macosx-ppc32-altivec:
	$(LN) ppc32alt.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="-c -Wall -fomit-frame-pointer" \
		OPT_NORMAL="-fast -mcpu=7450" \
		OPT_INLINE="-fast -mcpu=7450 -finline-limit=4000 -faltivec -maltivec"

# The -cross targets can be used to compile PowerPC binaries on x86.
macosx-ppc32-altivec-cross:
	$(LN) ppc32alt.h arch.h
	$(MAKE) $(PROJ) \
		ASFLAGS="$(ASFLAGS) -arch ppc" \
		CFLAGS="-c -Wall -arch ppc -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -arch ppc" \
		OPT_NORMAL="-fast -mcpu=7450" \
		OPT_INLINE="-fast -mcpu=7450 -finline-limit=4000 -faltivec -maltivec"

# "cc -traditional-cpp" was needed on older versions of Mac OS X; it might
# actually be problematic on current ones, but those will hopefully use other
# make targets anyway (e.g., macosx-ppc32-altivec above).
macosx-ppc32:
	$(LN) ppc32.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -traditional-cpp" \
		OPT_NORMAL="-O2" \
		OPT_INLINE="-O3"

macosx-ppc32-cross:
	$(LN) ppc32.h arch.h
	$(MAKE) $(PROJ) \
		ASFLAGS="$(ASFLAGS) -arch ppc" \
		CFLAGS="-c -Wall -arch ppc -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -arch ppc" \
		OPT_NORMAL="-O2" \
		OPT_INLINE="-O3 -finline-limit=4000"

# This is slightly slower than macosx-ppc32-altivec for most hash types.
macosx-ppc64-altivec:
	$(LN) ppc64alt.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="-c -m64 -Wall -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -m64" \
		OPT_NORMAL="-fast" \
		OPT_INLINE="-fast -finline-limit=4000 -faltivec -maltivec"

macosx-ppc64-altivec-cross:
	$(LN) ppc64alt.h arch.h
	$(MAKE) $(PROJ) \
		ASFLAGS="$(ASFLAGS) -arch ppc" \
		CFLAGS="-c -arch ppc -m64 -Wall -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -arch ppc -m64" \
		OPT_NORMAL="-fast" \
		OPT_INLINE="-fast -finline-limit=4000 -faltivec -maltivec"

macosx-ppc64:
	$(LN) ppc64.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="-c -m64 -Wall -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -m64" \
		OPT_NORMAL="-fast" \
		OPT_INLINE="-fast -finline-limit=4000"

macosx-ppc64-cross:
	$(LN) ppc64.h arch.h
	$(MAKE) $(PROJ) \
		ASFLAGS="$(ASFLAGS) -arch ppc" \
		CFLAGS="-c -arch ppc -m64 -Wall -fomit-frame-pointer" \
		LDFLAGS="$(LDFLAGS) -arch ppc -m64" \
		OPT_NORMAL="-fast" \
		OPT_INLINE="-fast -finline-limit=4000"

hpux-pa-risc-gcc:
	$(LN) pa-risc.h arch.h
	$(MAKE) $(PROJ) \
		CFLAGS="-c -Wall -O3 -fomit-frame-pointer"

hpux-pa-risc-cc:
	$(LN) pa-risc.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -Aa -D_HPUX_SOURCE -DANSI_CPP" \
		LDFLAGS="-s" \
		OPT_NORMAL="+O2" \
		OPT_INLINE="+O3 +Oinline"

irix-mips64-r10k:
	$(LN) mips64.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -O2 -64 -mips4 -r10000 -signed" \
		LDFLAGS="-s -64 -mips4 -r10000" \
		OPT_NORMAL="-LNO:opt=1 -OPT:Olimit=2194" \
		OPT_INLINE="-INLINE:all"

irix-mips64:
	$(LN) mips64.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -O2 -64 -mips3 -signed" \
		LDFLAGS="-s -64 -mips3" \
		OPT_NORMAL="-LNO:opt=1 -OPT:Olimit=2194" \
		OPT_INLINE="-INLINE:all"

irix-mips32:
	$(LN) mips32.h arch.h
	$(MAKE) $(PROJ) \
		CC=cc \
		CFLAGS="-c -O2 -32 -signed" \
		LDFLAGS="-s -32" \
		OPT_NORMAL="-LNO:opt=1 -OPT:Olimit=2194" \
		OPT_INLINE="-INLINE:all"

win32-cygwin-x86-sse2:
	$(CP) x86-sse.h arch.h
	$(MAKE) $(PROJ_WIN32) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-sse.o" \
		CFLAGS="$(CFLAGS) -mpreferred-stack-boundary=2" \
		ASFLAGS="$(ASFLAGS) -DUNDERSCORES"

win32-cygwin-x86-mmx:
	$(CP) x86-mmx.h arch.h
	$(MAKE) $(PROJ_WIN32) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-mmx.o" \
		CFLAGS="$(CFLAGS) -mpreferred-stack-boundary=2" \
		ASFLAGS="$(ASFLAGS) -DUNDERSCORES"

win32-cygwin-x86-any:
	$(CP) x86-any.h arch.h
	$(MAKE) $(PROJ_WIN32) \
		BIT_OBJS="$(BIT_OBJS) x86.o" \
		CFLAGS="$(CFLAGS) -mpreferred-stack-boundary=2" \
		ASFLAGS="$(ASFLAGS) -DUNDERSCORES"

beos-x86-sse2:
	$(LN) x86-sse.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-sse.o"

beos-x86-mmx:
	$(LN) x86-mmx.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o x86-mmx.o"

beos-x86-any:
	$(LN) x86-any.h arch.h
	$(MAKE) $(PROJ) \
		BIT_OBJS="$(BIT_OBJS) x86.o"

../bitripper: $(BIT_OBJS)
	$(LD) $(BIT_OBJS) $(LDFLAGS) -o ../bitripper

../bitripper.exe: $(BIT_OBJS)
	$(LD) $(BIT_OBJS) -lkernel32 -o ../bitripper.exe
	strip ../bitripper.exe

# Inlining the S-boxes produces faster code as long as they fit in the cache.
DES_bs_b.o: DES_bs_b.c sboxes.c nonstd.c sboxes-s.c
	$(CC) $(CFLAGS) $(OPT_INLINE) DES_bs_b.c

miscnl.o: misc.c
	$(CC) $(CFLAGS) $(OPT_NORMAL) -D_JOHN_MISC_NO_LOG misc.c -o miscnl.o

.c.o:
	$(CC) $(CFLAGS) $(OPT_NORMAL) $*.c

.S.o:
	$(AS) $(ASFLAGS) $*.S

depend:
	makedepend -fMakefile.dep -Y *.c 2>> /dev/null

clean:
	$(RM) $(PROJ) $(PROJ_WIN32)
	$(RM) ../bitripper *.o *.bak core
	$(RM) detect bench generic.h arch.h tmp.s
	$(CP) $(NULL) Makefile.dep

include Makefile.dep