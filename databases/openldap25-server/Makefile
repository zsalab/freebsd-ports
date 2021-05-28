# Created by: Xin LI <delphij@FreeBSD.org>

PORTNAME=		openldap
DISTVERSION=		2.5.4
PORTREVISION=		${OPENLDAP_PORTREVISION}
CATEGORIES=		net databases
MASTER_SITES=		https://www.openldap.org/software/download/OpenLDAP/%SUBDIR%/ \
			http://gpl.savoirfairelinux.net/pub/mirrors/openldap/%SUBDIR%/ \
			http://repository.linagora.org/OpenLDAP/%SUBDIR%/ \
			http://mirror.eu.oneandone.net/software/openldap/%SUBDIR%/ \
			ftp://ftp.ntua.gr/mirror/OpenLDAP/%SUBDIR%/ \
			https://mirror-hk.koddos.net/OpenLDAP/%SUBDIR%/ \
			ftp://ftp.dti.ad.jp/pub/net/OpenLDAP/%SUBDIR%/ \
			https://mirror.koddos.net/OpenLDAP/%SUBDIR%/ \
			https://mirror.lyrahosting.com/OpenLDAP/%SUBDIR%/ \
			ftp://ftp.OpenLDAP.org/pub/OpenLDAP/%SUBDIR%/ \
			http://www.openldap.org/software/download/OpenLDAP/%SUBDIR%/
MASTER_SITE_SUBDIR=	openldap-release
.if defined(CLIENT_ONLY)
.if ${CLIENT_ONLY} == sasl
PKGNAMESUFFIX=		-sasl-client
.else
PKGNAMESUFFIX=		-client
.endif
.else
PKGNAMESUFFIX?=		-server
.endif

MAINTAINER=		delphij@FreeBSD.org
.if defined(CLIENT_ONLY)
.if ${CLIENT_ONLY} == sasl
COMMENT=		Open source LDAP client implementation with SASL2 support
.else
COMMENT=		Open source LDAP client implementation
.endif
.else
COMMENT=		Open source LDAP server implementation
.endif

LICENSE=		OPENLDAP
LICENSE_NAME=		OpenLDAP Public License
LICENSE_FILE=		${WRKSRC}/LICENSE
LICENSE_PERMS=		dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

.if defined(CLIENT_ONLY)
.if ${CLIENT_ONLY} == sasl
CONFLICTS=		${PKGNAMEPREFIX}${PORTNAME}-client-2.* \
			${PKGNAMEPREFIX}${PORTNAME}-sasl-client-2.[0-4].*
.else
CONFLICTS=		${PKGNAMEPREFIX}${PORTNAME}-client-2.[0-4].* \
			${PKGNAMEPREFIX}${PORTNAME}-sasl-client-2.*
.endif
.endif

GNU_CONFIGURE=		yes
# :keepla because port uses lt_dlopen
USES=			cpe libtool:keepla ssl tar:tgz
.if !defined(CLIENT_ONLY)
USERS=			ldap
GROUPS=			ldap
LDAP_USER?=		ldap
LDAP_GROUP?=		ldap
.endif

WANT_OPENLDAP_VER?=	25
.if ${WANT_OPENLDAP_VER} != 25
BROKEN=			incompatible OpenLDAP version: ${WANT_OPENLDAP_VER}
.endif

PORTREVISION_CLIENT=	0
PORTREVISION_SERVER=	0
OPENLDAP_SHLIB_MAJOR=	2
OPENLDAP_SHLIB_MINOR=	5.4
OPENLDAP_MAJOR=		${DISTVERSION:R}

OPTIONS_DEFINE=		DEBUG FETCH GSSAPI

FETCH_DESC=		Enable fetch(3) support
GSSAPI_DESC=		With GSSAPI support (implies SASL support)

.if defined(CLIENT_ONLY)
OPTIONS_DEFINE+=	DOCS
.else

### Server Options ###

# General settings
OPTIONS_DEFINE+=	SASL DYNACL ACI RLOOKUPS SLP SLAPI TCP_WRAPPERS
OPTIONS_DEFINE+=	DYNAMIC_MODULES

# Backends
OPTIONS_DEFINE+=	BACKEND_DNSSRV BACKEND_LDAP BACKEND_MDB BACKEND_META 
OPTIONS_DEFINE+=	BACKEND_ASYNCMETA BACKEND_NDB BACKEND_NULL BACKEND_PASSWD
OPTIONS_DEFINE+=	BACKEND_PERL BACKEND_RELAY BACKEND_SOCK BACKEND_SQL
# TODO add missing libwiredtiger to ports
# OPTIONS_DEFINE+=	BACKEND_WT

# Overlays
OPTIONS_DEFINE+=	OVERLAY_ACCESSLOG OVERLAY_AUDITLOG OVERLAY_COLLECT
OPTIONS_DEFINE+=	OVERLAY_CONSTRAINT OVERLAY_DDS OVERLAY_DEREF OVERLAY_DYNGROUP
OPTIONS_DEFINE+=	OVERLAY_DYNLIST OVERLAY_MEMBEROF OVERLAY_PPOLICY OVERLAY_PCACHE
OPTIONS_DEFINE+=	OVERLAY_REFINT OVERLAY_RETCODE OVERLAY_RWM OVERLAY_SEQMOD
OPTIONS_DEFINE+=	OVERLAY_SSSVLV OVERLAY_SYNCPROV OVERLAY_TRANSLUCENT
OPTIONS_DEFINE+=	OVERLAY_UNIQUE OVERLAY_VALSORT
# Contrib overlays
OPTIONS_DEFINE+=	OVERLAY_LASTBIND OVERLAY_SMBPWD

# Password format support
OPTIONS_DEFINE+=	PW_CLEARTEXT PW_CRYPT
# Password modules
OPTIONS_DEFINE+=	PWHASH_SHA2 PWHASH_ARGON2 PWHASH_PBKDF2

# Misc
OPTIONS_DEFINE+=	PATCH_OUTLOOK

### Option Defaults ###

# General settings
OPTIONS_DEFAULT=	DYNAMIC_MODULES DYNACL ACI
# Backend modules
OPTIONS_DEFAULT+=	BACKEND_DNSSRV BACKEND_LDAP BACKEND_MDB BACKEND_META
OPTIONS_DEFAULT+=	BACKEND_ASYNCMETA BACKEND_NULL BACKEND_PASSWD
OPTIONS_DEFAULT+=	BACKEND_RELAY BACKEND_SOCK
# Overlay modules
OPTIONS_DEFAULT+=	OVERLAY_ACCESSLOG OVERLAY_AUDITLOG OVERLAY_COLLECT OVERLAY_CONSTRAINT
OPTIONS_DEFAULT+=	OVERLAY_DDS OVERLAY_DYNLIST OVERLAY_MEMBEROF OVERLAY_PCACHE OVERLAY_PPOLICY
OPTIONS_DEFAULT+=	OVERLAY_REFINT OVERLAY_RETCODE OVERLAY_RWM OVERLAY_SOCK OVERLAY_SSSVLV
OPTIONS_DEFAULT+=	OVERLAY_SYNCPROV OVERLAY_TRANSLUCENT OVERLAY_UNIQUE OVERLAY_VALSORT
# Password format
OPTIONS_DEFAULT+=	PW_CRYPT
# Password modules
OPTIONS_DEFAULT+=	PWHASH_SHA2 PWHASH_ARGON2 PWHASH_PBKDF2

### Option descriptions ###

DYNAMIC_MODULES_DESC=	Build dynamic backend and overlay modules
DYNACL_DESC=		Run-time loadable ACL
ACI_DESC=		Per-object ACI
RLOOKUPS_DESC=		With reverse lookups of client hostnames
SLP_DESC=		With SLPv2 (RFC 2608) support
SLAPI_DESC=		With Netscape SLAPI plugin API (experimental)
TCP_WRAPPERS_DESC=	With tcp wrapper support
SASL_DESC=		With (Cyrus) SASL2 support

BACKEND_MDB_DESC=		With Memory-Mapped DB backend
BACKEND_DNSSRV_DESC=		With Dnssrv backend
BACKEND_PASSWD_DESC=		With Passwd backend
BACKEND_PERL_DESC=		With Perl backend (DEPRECATED)
BACKEND_RELAY_DESC=		With Relay backend
BACKEND_SOCK_DESC=		With Sock backend
BACKEND_SQL_DESC=		With SQL backend (DEPRECATED)
BACKEND_LDAP_DESC=		With LDAP backend
BACKEND_META_DESC=		With Metadirectory backend
BACKEND_ASYNCMETA_DESC=	With Asynchronous metadirectory backend
BACKEND_NULL_DESC=		With Null backend
BACKEND_NDB_DESC=		With MySQL NDB Cluster backend (DEPRECATED)
BACKEND_WT_DESC=			With WiredTiger backend (experimental)

OVERLAY_ACCESSLOG_DESC=		With In-Directory Access Logging overlay
OVERLAY_AUDITLOG_DESC=		With Audit Logging overlay
OVERLAY_COLLECT_DESC=		With Collect overy Services overlay
OVERLAY_CONSTRAINT_DESC=	With Attribute Constraint overlay
OVERLAY_DDS_DESC=		With Dynamic Directory Services overlay
OVERLAY_DEREF_DESC=		With Dereference overlay
OVERLAY_DYNGROUP_DESC=		With Dynamic Group overlay (DEPRECATED)
OVERLAY_DYNLIST_DESC=		With Dynamic List overlay
OVERLAY_MEMBEROF_DESC=		With Reverse Group Membership overlay
OVERLAY_PPOLICY_DESC=		With Password Policy overlay
OVERLAY_PCACHE_DESC=		With Proxy Cache overlay
OVERLAY_REFINT_DESC=		With Referential Integrity overlay
OVERLAY_RETCODE_DESC=		With Return Code testing overlay
OVERLAY_RWM_DESC=		With Rewrite/Remap overlay
OVERLAY_SEQMOD_DESC=		With Sequential Modify overlay
OVERLAY_SSSVLV_DESC=		With ServerSideSort/VLV overlay
OVERLAY_SYNCPROV_DESC=		With Syncrepl Provider overlay
OVERLAY_TRANSLUCENT_DESC=	With Translucent Proxy overlay
OVERLAY_UNIQUE_DESC=		With attribute Uniqueness overlay
OVERLAY_VALSORT_DESC=		With Value Sorting overlay
OVERLAY_SMBPWD_DESC=		With Samba Password hashes overlay
OVERLAY_LASTBIND_DESC=		With lastbind overlay

PW_CLEARTEXT_DESC=		With cleartext password support
PW_CRYPT_DESC=		With crypt(3) password support
PWHASH_SHA2_DESC=		With SHA2 password hashing module
PWHASH_ARGON2_DESC=		With Argon2 password hashing module
PWHASH_PBKDF2_DESC=		With PBKDF2 password hashing module

PATCH_OUTLOOK_DESC=		Force caseIgnoreOrderingMatch on name attribute (experimental)
.endif

.if defined(CLIENT_ONLY)
OPENLDAP_PORTREVISION=	${PORTREVISION_CLIENT}
OPENLDAP_PKGFILESUFX=	.client
.else
OPENLDAP_PORTREVISION=	${PORTREVISION_SERVER}
OPENLDAP_PKGFILESUFX=
.endif

CONFIGURE_SED=		-e 's,uuid/uuid.h,xxuuid/uuid.h,g'

.include <bsd.port.options.mk>

.if defined(CLIENT_ONLY)
PORTDOCS=		CHANGES drafts rfc

.if ${CLIENT_ONLY} == sasl
PORT_OPTIONS+=	SASL
.endif
.if defined(USE_OPENLDAP)
BROKEN=			you have USE_OPENLDAP variable defined either in environment or in make(1) arguments; please undefine and try again
.endif
.else
USE_OPENLDAP=		yes
WANT_OPENLDAP_VER=	25

LIB_DEPENDS+=		libicudata.so:devel/icu

.if ${PORT_OPTIONS:MGSSAPI} && empty(PORT_OPTIONS:MSASL)
PORT_OPTIONS+=	SASL
.endif

.if ${PORT_OPTIONS:MSASL}
WANT_OPENLDAP_SASL=	yes
CONFLICTS=		${PKGNAMEPREFIX}${PORTNAME}-client-2.*
PKGNAMESUFFIX=		-sasl-server
.if ${PORT_OPTIONS:MGSSAPI}
RUN_DEPENDS+=		cyrus-sasl-gssapi>0:security/cyrus-sasl2-gssapi
.endif
.else
CONFLICTS=		${PKGNAMEPREFIX}${PORTNAME}-sasl-client-2.*
.endif

.endif

DESCR=			${PKGDIR}/pkg-descr${OPENLDAP_PKGFILESUFX}
PLIST=			${PKGDIR}/pkg-plist${OPENLDAP_PKGFILESUFX}

LDAP_RUN_DIR?=		/var/run/openldap
LOCALSTATEDIR?=		/var/db
DATABASEDIR?=		${LOCALSTATEDIR}/openldap-data

SUB_LIST+=		LDAP_RUN_DIR=${LDAP_RUN_DIR} \
			LDAP_USER=${LDAP_USER} \
			LDAP_GROUP=${LDAP_GROUP} \
			DATABASEDIR=${DATABASEDIR} \
			PKGNAME=${PKGNAME}

CONFIGURE_ARGS=		--with-threads=posix \
			--with-tls=openssl \
			--disable-dependency-tracking \
			--enable-dynamic

.if ${PORT_OPTIONS:MSASL}
LIB_DEPENDS+=		libsasl2.so:security/cyrus-sasl2
CONFIGURE_ARGS+=	--with-cyrus-sasl
.else
CONFIGURE_ARGS+=	--without-cyrus-sasl
.endif

.if defined(CLIENT_ONLY)
# client specific configuration

CONFIGURE_ARGS+=	--disable-slapd \
			--disable-relay \
			--disable-syncprov
SUB_FILES+=		pkg-message.client
PKGMESSAGE=		${WRKSRC}/pkg-message.client

USE_LDCONFIG=		yes

.else
# server specific configuration

USE_LDCONFIG=		${PREFIX}/libexec/openldap
SUB_FILES+=		pkg-message pkg-deinstall
USE_RC_SUBR=		slapd

EXTRA_PATCHES+=		${FILESDIR}/extrapatch-Makefile.in

MAKE_ENV+=		STRIP=${STRIP}

CONFIGURE_ARGS+=	--localstatedir=${LOCALSTATEDIR} \
			--enable-crypt

.if ${PORT_OPTIONS:MACI}
.if ${PORT_OPTIONS:MDYNAMIC_MODULES}
CONFIGURE_ARGS+=	--enable-aci=mod
ACI_PLIST=		""
.else
CONFIGURE_ARGS+=	--enable-aci=yes
ACI_PLIST=		"@comment "
.endif
.endif

.if ${PORT_OPTIONS:MDYNACL}
CONFIGURE_ARGS+=	--enable-dynacl
.endif

.if ${PORT_OPTIONS:MDEBUG}
CONFIGURE_ARGS+=	--enable-debug=yes
.endif

.if ${PORT_OPTIONS:MRLOOKUPS}
CONFIGURE_ARGS+=	--enable-rlookups
PLIST_SUB+=		RLOOKUPS=""
.else
PLIST_SUB+=		RLOOKUPS="@comment "
.endif

.if ${PORT_OPTIONS:MSLAPI}
CONFIGURE_ARGS+=	--enable-slapi
PLIST_SUB+=		SLAPI=""
USE_LDCONFIG=		yes
.else
PLIST_SUB+=		SLAPI="@comment "
.endif

.if ${PORT_OPTIONS:MSLP}
CONFIGURE_ARGS+=	--enable-slp
LIB_DEPENDS+=		libslp.so:net/openslp
.endif

# Include tcp-wrapper support
.if ${PORT_OPTIONS:MTCP_WRAPPERS}
CONFIGURE_ARGS+=	--enable-wrappers
.endif

.if ${PORT_OPTIONS:MSASL}
CONFIGURE_ARGS+=	--enable-spasswd
.endif

.if ${PORT_OPTIONS:MPW_CLEARTEXT}
CONFIGURE_ARGS+=	--enable-cleartext
.else
CONFIGURE_ARGS+=	--disable-cleartext
.endif

.if ${PORT_OPTIONS:MPW_CRYPT}
CONFIGURE_ARGS+=	--enable-crypt
.endif

.if ${PORT_OPTIONS:MDYNAMIC_MODULES} || ${PORT_OPTIONS:MSLAPI}
LIB_DEPENDS+=		libltdl.so:devel/libltdl
LDFLAGS+=		-L${LOCALBASE}/lib
CONFIGURE_ARGS+=	--enable-modules
PLIST_SUB+=		MODULES=""
.else
PLIST_SUB+=		MODULES="@comment "
.endif

.if ${PORT_OPTIONS:MDYNAMIC_MODULES}
MODULE_ENABLE=		"mod"
MODULE_PLIST=		""
.else
MODULE_ENABLE=		"yes"
MODULE_PLIST=		"@comment "
.endif

# Backends begin

.if ${PORT_OPTIONS:MBACKEND_DNSSRV}
CONFIGURE_ARGS+=	--enable-dnssrv=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_DNSSRV=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_DNSSRV="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_MDB}
CONFIGURE_ARGS+=	--enable-mdb=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_MDB=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_MDB="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_PASSWD}
CONFIGURE_ARGS+=	--enable-passwd=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_PASSWD=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_PASSWD="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_RELAY}
CONFIGURE_ARGS+=	--enable-relay=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_RELAY=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_RELAY="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_SOCK}
CONFIGURE_ARGS+=	--enable-sock=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_SOCK=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_SOCK="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_PERL}
USES+=			perl5
CONFIGURE_ARGS+=	--enable-perl=${MODULE_ENABLE}
CONFIGURE_ENV+=		PERLBIN="${PERL}"
PLIST_SUB+=		BACKEND_PERL=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_PERL="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_LDAP}
CONFIGURE_ARGS+=	--enable-ldap=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_LDAP=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_LDAP="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_META}
CONFIGURE_ARGS+=	--enable-meta=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_META=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_META="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_ASYNCMETA}
CONFIGURE_ARGS+=	--enable-asyncmeta=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_ASYNCMETA=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_ASYNCMETA="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_NULL}
CONFIGURE_ARGS+=	--enable-null=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_NULL=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_NULL="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_NDB}
CONFIGURE_ARGS+=	--enable-ndb=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_NDB=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_NDB="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_WT}
# TODO add missing libwiredtiger to ports
CONFIGURE_ARGS+=	--enable-wt=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_WT=${MODULE_PLIST}
.else
PLIST_SUB+=		BACKEND_WT="@comment "
.endif

.if ${PORT_OPTIONS:MBACKEND_SQL}
CONFIGURE_ARGS+=	--enable-sql=${MODULE_ENABLE}
PLIST_SUB+=		BACKEND_SQL=${MODULE_PLIST}
LIB_DEPENDS+=		libodbc.so:databases/unixODBC
LDFLAGS+=		-L${LOCALBASE}/lib
.else
PLIST_SUB+=		BACKEND_SQL="@comment "
.endif

# End of backends

# Overlays

.if ${PORT_OPTIONS:MOVERLAY_ACCESSLOG}
CONFIGURE_ARGS+=	--enable-accesslog=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_ACCESSLOG=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_ACCESSLOG="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_AUDITLOG}
CONFIGURE_ARGS+=	--enable-auditlog=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_AUDITLOG=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_AUDITLOG="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_COLLECT}
CONFIGURE_ARGS+=	--enable-collect=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_COLLECT=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_COLLECT="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_CONSTRAINT}
CONFIGURE_ARGS+=	--enable-constraint=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_CONSTRAINT=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_CONSTRAINT="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_DDS}
CONFIGURE_ARGS+=	--enable-dds=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_DDS=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_DDS="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_DEREF}
CONFIGURE_ARGS+=	--enable-deref=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_DEREF=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_DEREF="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_DYNGROUP}
CONFIGURE_ARGS+=	--enable-dyngroup=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_DYNGROUP=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_DYNGROUP="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_DYNLIST}
CONFIGURE_ARGS+=	--enable-dynlist=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_DYNLIST=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_DYNLIST="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_MEMBEROF}
CONFIGURE_ARGS+=	--enable-memberof=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_MEMBEROF=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_MEMBEROF="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_PPOLICY}
CONFIGURE_ARGS+=	--enable-ppolicy=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_PPOLICY=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_PPOLICY="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_PCACHE}
CONFIGURE_ARGS+=	--enable-proxycache=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_PCACHE=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_PCACHE="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_REFINT}
CONFIGURE_ARGS+=	--enable-refint=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_REFINT=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_REFINT="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_RETCODE}
CONFIGURE_ARGS+=	--enable-retcode=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_RETCODE=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_RETCODE="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_RWM}
CONFIGURE_ARGS+=	--enable-rwm=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_RWM=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_RWM="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_SEQMOD}
CONFIGURE_ARGS+=	--enable-seqmod=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_SEQMOD=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_SEQMOD="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_SSSVLV}
CONFIGURE_ARGS+=	--enable-sssvlv=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_SSSVLV=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_SSSVLV="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_SYNCPROV}
CONFIGURE_ARGS+=	--enable-syncprov=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_SYNCPROV=${MODULE_PLIST}
.else
CONFIGURE_ARGS+=	--disable-syncprov
PLIST_SUB+=		OVERLAY_SYNCPROV="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_TRANSLUCENT}
CONFIGURE_ARGS+=	--enable-translucent=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_TRANSLUCENT=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_TRANSLUCENT="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_UNIQUE}
CONFIGURE_ARGS+=	--enable-unique=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_UNIQUE=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_UNIQUE="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_VALSORT}
CONFIGURE_ARGS+=	--enable-valsort=${MODULE_ENABLE}
PLIST_SUB+=		OVERLAY_VALSORT=${MODULE_PLIST}
.else
PLIST_SUB+=		OVERLAY_VALSORT="@comment "
.endif

.if ${PORT_OPTIONS:MOVERLAY_LASTBIND}
PLIST_SUB+=		LASTBIND=""
.else
PLIST_SUB+=		LASTBIND="@comment "
.endif


.if ${PORT_OPTIONS:MOVERLAY_SMBPWD}
PLIST_SUB+=		SMBPWD=""
.else
PLIST_SUB+=		SMBPWD="@comment "
.endif

# End of overlays

# Password hash modules

.if ${PORT_OPTIONS:MPWHASH_ARGON2}
LIB_DEPENDS+=		libsodium.so:security/libsodium
LDFLAGS+=		-L${LOCALBASE}/lib
CONFIGURE_ARGS+=	--enable-argon2
.endif

.if ${PORT_OPTIONS:MPWHASH_SHA2}
PLIST_SUB+=		SHA2=""
.else
PLIST_SUB+=		SHA2="@comment "
.endif

.if ${PORT_OPTIONS:MPWHASH_PBKDF2}
PLIST_SUB+=		PBKDF2=""
.else
PLIST_SUB+=		PBKDF2="@comment "
.endif

# End of password hash modules

# Misc

# Force using caseIgnoreOrderingMatch on 'name' attribute.
# This may be a violation of RFC 4519 2.18 definition.
# See http://www.openldap.org/lists/openldap-technical/201211/msg00175.html
.if ${PORT_OPTIONS:MPATCH_OUTLOOK}
EXTRA_PATCHES+=		${FILESDIR}/extrapatch-outlook-servers__slapd__schema_prep.c
.endif

# end of client/server specific configuration
.endif

.if defined(WITH_CLDAP)
CPPFLAGS+=		-DLDAP_CONNECTIONLESS
.endif

CPPFLAGS+=		-I${LOCALBASE}/include
LIBS+=			-L${LOCALBASE}/lib

.if defined(CLIENT_ONLY)
.else
SUB_LIST+=		RC_DIR=${PREFIX} \
			LDAP_RUN_DIR=${LDAP_RUN_DIR} \
			DATABASEDIR=${DATABASEDIR}
.endif

PLIST_SUB+=		${SUB_LIST}
PLIST_SUB+=		SHLIB_MAJOR=${OPENLDAP_SHLIB_MAJOR}
PLIST_SUB+=		SHLIB_MINOR=${OPENLDAP_SHLIB_MINOR}
PLIST_SUB+=		OPENLDAP_MAJOR=${OPENLDAP_MAJOR}

.include <bsd.port.pre.mk>

.if !${PORT_OPTIONS:MFETCH}
CONFIGURE_ARGS+=	--without-fetch
.else
. if defined(OPENSSL_INSTALLED) && ${OPENSSL_INSTALLED} != "" || ${SSL_DEFAULT} != base
BROKEN=	using OpenSSL from ports and OPTION FETCH together is not supported
. endif
.endif

SED_MODULES=		-e 's/\(moduleload[ 	]*back_[a-z]*\)\.la/\1/'

post-patch:
	@${REINPLACE_CMD} -e 's|%LOCALSTATEDIR%/run/|${LDAP_RUN_DIR}/|g' \
		${SED_MODULES} ${WRKSRC}/servers/slapd/slapd.conf
	@${REINPLACE_CMD} -e 's|^OPT =.*|OPT = ${CFLAGS}|g' \
		-e 's|^CC =.*|CC = ${CC}|g' \
		${SED_MODULES} ${WRKSRC}/contrib/slapd-modules/*/Makefile \
		${WRKSRC}/contrib/slapd-modules/*/*/Makefile
.if defined(CONFIGURE_SED)
	@${REINPLACE_CMD} -E ${CONFIGURE_SED} \
		${CONFIGURE_WRKSRC}/${CONFIGURE_SCRIPT}
.endif

pre-configure:
	@if [ -n "`${PKG_INFO} -xI '^bind\(84\)\{0,1\}-base-8\.' 2>/dev/null`" ]; then \
		${ECHO_CMD} "${PKGNAME}: bind installed with PORT_REPLACES_BASE_BIND causes build problems."; \
		${FALSE}; \
	fi

.if !defined(CLIENT_ONLY)
test: build
	@(cd ${BUILD_WRKSRC} && ${SETENV} ${MAKE_ENV} \
		${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} ${MAKE_ARGS} test)

post-build:
	@${DO_NADA}
.if ${PORT_OPTIONS:MSMBPWD}
	@(cd ${BUILD_WRKSRC}/contrib/slapd-modules/smbk5pwd && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} DEFS="-DDO_SAMBA" prefix="${PREFIX}" all)
.endif
.if ${PORT_OPTIONS:MPWHASH_SHA2}
	@(cd ${BUILD_WRKSRC}/contrib/slapd-modules/passwd/sha2 && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" all)
.endif
.if ${PORT_OPTIONS:MPWHASH_PBKDF2}
	@(cd ${BUILD_WRKSRC}/contrib/slapd-modules/passwd/pbkdf2 && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" all)
.endif

.if ${PORT_OPTIONS:MLASTBIND}
	@(cd ${BUILD_WRKSRC}/contrib/slapd-modules/lastbind && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" all)
.endif
.endif

pre-install:
.if !defined(CLIENT_ONLY)
	${MKDIR} ${STAGEDIR}${DATABASEDIR}
.endif

post-install:
.if defined(CLIENT_ONLY)
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/CHANGES ${STAGEDIR}${DOCSDIR}
	for dir in drafts rfc; do \
		${MKDIR} ${STAGEDIR}${DOCSDIR}/$${dir}; \
		${INSTALL_DATA} ${WRKSRC}/doc/$${dir}/* ${STAGEDIR}${DOCSDIR}/$${dir}; \
	done
	for prog in ldapcompare ldapdelete ldapexop ldapmodify ldapmodrdn ldappasswd ldapsearch ldapurl ldapwhoami; do\
		${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/$${prog}; \
	done

	for library in lber ldap ldap_r; do \
		${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/lib$${library}-${OPENLDAP_MAJOR}.so.${OPENLDAP_SHLIB_MAJOR}; \
	done
.else
	${MKDIR} ${STAGEDIR}${LDAP_RUN_DIR}
.if ${PORT_OPTIONS:MSMBPWD}
	(cd ${WRKSRC}/contrib/slapd-modules/smbk5pwd && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" install)
	${RM} ${STAGEDIR}${PREFIX}/libexec/openldap/smbk5pwd.a
.endif
.if ${PORT_OPTIONS:MPWHASH_SHA2}
	(cd ${WRKSRC}/contrib/slapd-modules/passwd/sha2 && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" install)
	${RM} ${STAGEDIR}${PREFIX}/libexec/openldap/pw-sha2.a
.endif
.if ${PORT_OPTIONS:MPWHASH_PBKDF2}
	(cd ${WRKSRC}/contrib/slapd-modules/passwd/pbkdf2 && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" install)
	${RM} ${STAGEDIR}${PREFIX}/libexec/openldap/pw-pbkdf2.a
.endif

.if ${PORT_OPTIONS:MLASTBIND}
	(cd ${WRKSRC}/contrib/slapd-modules/lastbind && \
		${SETENV} ${MAKE_ENV} ${MAKE_CMD} ${MAKE_FLAGS} ${MAKEFILE} \
		${MAKE_ARGS} prefix="${PREFIX}" install)
	${RM} ${STAGEDIR}${PREFIX}/libexec/openldap/lastbind.a
.endif
.if ${PORT_OPTIONS:MDYNAMIC_MODULES} || ${PORT_OPTIONS:MSMBPWD} || ${PORT_OPTIONS:MPWHASH_SHA2} || ${PORT_OPTIONS:MPWHASH_PBKDF2}
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/libexec/openldap/*.so
.endif
.if ${PORT_OPTIONS:MDYNAMIC_MODULES} || ${PORT_OPTIONS:MSLAPI}
	${MKDIR} ${STAGEDIR}${PREFIX}/libexec/openldap
.endif
.endif # defined(CLIENT_ONLY)

.include <bsd.port.post.mk>
