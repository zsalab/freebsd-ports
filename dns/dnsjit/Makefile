PORTNAME=	dnsjit
DISTVERSIONPREFIX=	v
DISTVERSION=	1.2.1
CATEGORIES=	dns net

PATCH_SITES=	https://github.com/DNS-OARC/dnsjit/commit/
PATCHFILES=	3cdd801153373a316027920e5c650f111777fab4.patch:-p1

MAINTAINER=	freebsd@dns.company
COMMENT=	Engine for capturing, parsing and replaying DNS

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libck.so:devel/concurrencykit \
		libgnutls.so:security/gnutls \
		liblmdb.so:databases/lmdb \
		libluajit-5.1.so:lang/luajit-openresty \
		liblz4.so:archivers/liblz4 \
		libpcap.so:net/libpcap \
		libzstd.so:archivers/zstd

USES=		autoreconf libtool pkgconfig
USE_GITHUB=	yes
GH_ACCOUNT=	DNS-OARC

GNU_CONFIGURE=	yes

OPTIONS_DEFINE=	EXAMPLES

post-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/*.lua ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
