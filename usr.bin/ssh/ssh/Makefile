#	$OpenBSD: Makefile,v 1.72 2018/01/08 15:37:38 markus Exp $

.PATH:		${.CURDIR}/..

SRCS=	ssh.c readconf.c clientloop.c sshtty.c sshconnect.c sshconnect2.c mux.c
SRCS+=	atomicio.c authfd.c bufaux.c buffer.c compat.c dns.c fatal.c \
	hostfile.c key.c msg.c readpass.c utf8.c
SRCS+=	${SRCS_BASE} ${SRCS_KEX} ${SRCS_KEXC} ${SRCS_KEY} ${SRCS_KEYP} \
	${SRCS_KRL} ${SRCS_PROT} ${SRCS_PKT} ${SRCS_UTL} ${SRCS_PKCS11}

PROG=	ssh
BINOWN=	root

#BINMODE?=4555

BINDIR=	/usr/bin
MAN=	ssh.1 ssh_config.5

.include <bsd.own.mk>

KERBEROS5=no

.if (${KERBEROS5:L} == "yes")
CFLAGS+= -DKRB5 -I${DESTDIR}/usr/include/kerberosV -DGSSAPI
.endif # KERBEROS5

.include <bsd.prog.mk>

.if (${KERBEROS5:L} == "yes")
DPADD+=  ${LIBGSSAPI} ${LIBKRB5}
LDADD+=  -lgssapi -lkrb5 -lasn1
LDADD+=  -lwind -lroken -lcom_err -lpthread -lheimbase
.endif # KERBEROS5

.if (${OPENSSL:L} == "yes")
LDADD+=	-lcrypto
DPADD+=	${LIBCRYPTO}
.endif

LDADD+=	-lutil -lz
DPADD+=	${LIBUTIL} ${LIBZ}
