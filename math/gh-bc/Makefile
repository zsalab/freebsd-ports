PORTNAME=	bc
PORTVERSION=	5.1.1
CATEGORIES=	math lang
PKGNAMEPREFIX=	gh-

MAINTAINER=	se@FreeBSD.org
COMMENT=	GNU compatible bc/dc calculator

LICENSE=	BSD2CLAUSE MIT
LICENSE_COMB=	multi
LICENSE_FILE=	${WRKSRC}/LICENSE.md

USES=		compiler:c11
USE_GITHUB=	yes
GH_ACCOUNT=	gavinhoward

HAS_CONFIGURE=		yes
CONFIGURE_SCRIPT=	configure.sh
CONFIGURE_ARGS=		-G
CFLAGS+=		-Dstatic_assert=_Static_assert

.include <bsd.port.pre.mk>

CONFLICTS_INSTALL=	gnubc

pre-build:
		${INSTALL_SCRIPT} ${WRKSRC}/gen/strgen.sh ${WRKSRC}/gen/strgen

do-install:
		${INSTALL_PROGRAM} ${WRKSRC}/bin/bc ${STAGEDIR}${PREFIX}/bin/
		${LN} ${STAGEDIR}${PREFIX}/bin/bc ${STAGEDIR}${PREFIX}/bin/dc
		${INSTALL_MAN} ${WRKSRC}/manuals/bc.1 ${STAGEDIR}${MANPREFIX}/share/man/man1
		${INSTALL_MAN} ${WRKSRC}/manuals/dc.1 ${STAGEDIR}${MANPREFIX}/share/man/man1
		${MKDIR} ${STAGEDIR}${PREFIX}/share/nls/C
		${WRKSRC}/scripts/locale_install.sh ${STAGEDIR}${PREFIX}/share/nls/%L/%N.cat ${PORTNAME}
		${MV} ${STAGEDIR}${PREFIX}/share/nls/en_US/bc.cat ${STAGEDIR}${PREFIX}/share/nls/C/
		${RMDIR} ${STAGEDIR}${PREFIX}/share/nls/en_US

do-test:
		${MAKE} -C ${WRKSRC} test

.include <bsd.port.post.mk>
