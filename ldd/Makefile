#	$NetBSD: Makefile,v 1.7.52.1 2009/01/16 22:21:30 bouyer Exp $

.include <bsd.own.mk>		# for MKDYNAMICROOT definition

PROG=	ldd
SRCS=	ldd.c
MAN=	ldd.1

SUBDIR=	aout elf32 elf64
LIB_AOUTDIR!=	cd ${.CURDIR}/aout && ${PRINTOBJDIR}
EXTRA_LIBS+=	${LIB_AOUTDIR}/libldd_aout.a

.if (${MACHINE_ARCH} != "alpha")
LIB_ELF32DIR!=	cd ${.CURDIR}/elf32 && ${PRINTOBJDIR}
EXTRA_LIBS+=	${LIB_ELF32DIR}/libldd_elf32.a
.endif

.if (${MACHINE_ARCH} == "alpha") || (${MACHINE_ARCH} == "sparc64") || \
    (${MACHINE_ARCH} == "x86_64") || (${MACHINE_ARCH} == "powerpc64")
LIB_ELF64DIR!=	cd ${.CURDIR}/elf64 && ${PRINTOBJDIR}
EXTRA_LIBS+=	${LIB_ELF64DIR}/libldd_elf64.a
CPPFLAGS.ldd.c= -DELFSIZE=64
.else
CPPFLAGS.ldd.c= -DELFSIZE=32
.endif

LDADD+=	${EXTRA_LIBS}
DPADD+=	${EXTRA_LIBS}

.include "Makefile.common"

.if (${MKDYNAMICROOT} == "no")
LDSTATIC?= -static
.endif

.include <bsd.prog.mk>
.include <bsd.subdir.mk>
