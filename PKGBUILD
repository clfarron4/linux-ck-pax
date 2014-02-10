# Maintainer: Duncan Townsend <duncant@mit.edu>
# Contributors of the linux PKGBUILD
#	Tobias Powalowski <tpowa@archlinux.org>
#	Thomas Baechler <thomas@archlinux.org>
# Contributor of the -ck PKGBUILD
#	graysky <graysky AT archlinux DOT us>
# Contributor of the -pax PKGBUILD
#	phects <phects@orgizm.net>

### BUILD OPTIONS
# Set these variables to ANYTHING that is not null to enable them

# Tweak kernel options prior to a build via nconfig
_makenconfig=

# Running with a 1000 HZ tick rate (vs the ARCH 300) is reported to solve the
# issues with the bfs/linux 3.1x and suspend. For more see:
# http://ck-hack.blogspot.com/2013/09/bfs-0441-311-ck1.html?showComment=1378756529345#c5266548105449573343
_1k_HZ_ticks=y

# NUMA is optimized for multi-socket motherboards.
# A single multi-core CPU actually runs slower with NUMA enabled.
# See, https://bugs.archlinux.org/task/31187
_NUMAdisable=y

# Compile ONLY probed modules
# As of mainline 2.6.32, running with this option will only build the modules
# that you currently have probed in your system VASTLY reducing the number of
# modules built and the build time to do it.
#
# WARNING - ALL modules must be probed BEFORE you begin making the pkg!
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: http://aur.archlinux.org/packages.php?ID=41689
# This PKGBUILD will call it directly to probe all the modules you have logged!
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed_db
_localmodcfg=

# Use the current kernel's .config file
# Enabling this option will use the .config of the RUNNING kernel rather than
# the ARCH defaults. Useful when the package gets updated and you already went
# through the trouble of customizing your config options.  NOT recommended when
# a new kernel is released, but again, convenient for package bumps.
_use_current=

# Alternative I/O scheduler by Paolo.
# Set this if you want it enabled globally i.e. for all devices in your system
# If you want it enabled on a device-by-device basis, leave this unset and see:
# https://wiki.archlinux.org/index.php/Linux-ck#How_to_Enable_the_BFQ_I.2FO_Scheduler
_BFQ_enable_=y

### Do no edit below this line unless you know what you're doing

pkgname=linux-ck-pax
true && pkgname=(linux-ck-pax linux-ck-pax-headers)
_kernelname=-ck-pax
_srcname=linux-3.12
pkgver=3.12.8
pkgrel=1
arch=('i686' 'x86_64')
url="https://wiki.archlinux.org/index.php/Linux-ck"
license=('GPL2')
makedepends=('kmod' 'inetutils' 'bc')
options=('!strip')
_ckpatchversion=2
_paxver=test15
_ckpatchname="patch-3.12-ck${_ckpatchversion}"
_gcc_patch="kernel-312-gcc48-1.patch"
_bfqpath="http://repo-ck.com/source/mirror"
source=("http://www.kernel.org/pub/linux/kernel/v3.x/${_srcname}.tar.xz"
        "http://www.kernel.org/pub/linux/kernel/v3.x/patch-${pkgver}.xz"
        "http://ck.kolivas.org/patches/3.0/3.12/3.12-ck${_ckpatchversion}/${_ckpatchname}.bz2"
        "http://repo-ck.com/source/gcc_patch/${_gcc_patch}.gz"
        'linux-ck-pax.preset'
        'change-default-console-loglevel.patch'
        'config' 'config.x86_64'
        'criu-no-expert.patch'
	'sunrpc-create-a-new-dummy-pipe-for-gssd-to-hold-open.patch'
	'sunrpc-replace-gssd_running-with-more-reliable-check.patch'
	'nfs-check-gssd-running-before-krb5i-auth.patch'
	'rpc_pipe-remove-the-clntXX-dir-if-creating-the-pipe-fails.patch'
	'sunrpc-add-an-info-file-for-the-dummy-gssd-pipe.patch'
	'rpc_pipe-fix-cleanup-of-dummy-gssd-directory-when-notification-fails.patch'
        "${_bfqpath}/0001-block-cgroups-kconfig-build-bits-for-BFQ-v7r1-3.12.patch"
        "${_bfqpath}/0002-block-introduce-the-BFQ-v7r1-I-O-sched-for-3.12.patch"
        "${_bfqpath}/0003-block-bfq-add-Early-Queue-Merge-EQM-to-BFQ-v7r1-for-3.12.0.patch"
        "pax-ck-${pkgver}-${_paxver}.patch"
        "http://grsecurity.net/test/pax-linux-${pkgver}-${_paxver}.patch")
sha256sums=('2e120ec7fde19fa51dc6b6cc11c81860a0775defcad5a5bf910ed9a50e845a02'
            'a8e056bec1a39bbca8d2df9c477a9dee0e263ae4335601548eda14326e83e782'
            '413def4af24ff70615cf5ef5cc1f1347bd634d87686a84ad0e2c2d3b052da8b8'
            'caf4d413bec6de71ac33b5eef578579452613c552412788c93b5de7dc6ee6899'
            'f126f7d4005b5d0adb61f0ccde95ac42baaf6f2bec14babd6d14935e377481b2'
            'faced4eb4c47c4eb1a9ee8a5bf8a7c4b49d6b4d78efbe426e410730e6267d182'
            '53f9afa9662b0b2e0f1ecbc47377ed11012cdc8844a70ccc080d91f50d3ec6f8'
            '208eabee0dd42a2a001ca6037eec39630feaa15f011e438c211657f9cfb17a94'
            'daa75228a4c45a925cc5dbfeba884aa696a973a26af7695adc198c396474cbd5'
            'b6f366ed2100ccab99029f61c39c0781ad4863f537381626196ed43b4b115a21'
            'cbfabd113a1954cd3d6cc1e70c19b95ce36a19e2c92ad93939d4982077178135'
            '139d576c540840fe18b0ce8468c243011e5f8b4aebfb1a288afe10b9f8d88137'
            'c045ce9c2571c4e6ff63345ea9abd9f778f56206f686b95491523ac740458420'
            'd8d6745a165e7f1608d8c298e49c8c2fee5a5d6c61c5b80d63a8dc7913ff8dc8'
            'fecca9a761f3427c7f2f793e5d9a34d6f43799143e9a6b51edc372f88c76022e'
            '87053ddc166c14f5726926bc7a218192b6525e64030d25711a1b4e913156ab44'
            '7460b296f0e379bb630eaac6d3e8a76eedcf30b490c5281e5fa75e2ddc0db94b'
            '43faef626341cb71be838070691b0d472df5f6f4faa6593376bd3eb2d0a30d15'
            'ab973d1700bd2b88242970ab6005e3c1ffa41a7061a4640affe27a54ee5653b2'
            'f85df0c702c88d64000f82f9043f62a858eea375cfe85c8770378c75d1f7c787')

prepare() {
	cd "${srcdir}"

	# patch PaX to play nice with BFS
	msg "Patching PaX to be compatible with BFS"
	patch --follow-symlinks -i "${srcdir}/pax-ck-${pkgver}-${_paxver}.patch" -o "${srcdir}/pax-linux-bfs-${pkgver}-${_paxver}.patch"

	cd "${_srcname}"

	# add upstream patch
	msg "Patching source upstream patch set to $pkgver"
	patch -p1 -i "${srcdir}/patch-${pkgver}"

	# set DEFAULT_CONSOLE_LOGLEVEL to 4 (same value as the 'quiet' kernel param)
	# remove this when a Kconfig knob is made available by upstream
	# (relevant patch sent upstream: https://lkml.org/lkml/2011/7/26/227)
	patch -Np1 -i "${srcdir}/change-default-console-loglevel.patch"

	# allow criu without expert option set
	# patch from fedora
	patch -Np1 -i "${srcdir}/criu-no-expert.patch"
	# fix 15 seocnds nfs delay
	patch -Np1 -i "${srcdir}/sunrpc-create-a-new-dummy-pipe-for-gssd-to-hold-open.patch"
	patch -Np1 -i "${srcdir}/sunrpc-replace-gssd_running-with-more-reliable-check.patch"
	patch -Np1 -i "${srcdir}/nfs-check-gssd-running-before-krb5i-auth.patch"
	# fix nfs kernel oops
	# #37866
	patch -Np1 -i "${srcdir}/rpc_pipe-remove-the-clntXX-dir-if-creating-the-pipe-fails.patch"
	patch -Np1 -i "${srcdir}/sunrpc-add-an-info-file-for-the-dummy-gssd-pipe.patch"

	patch -Np1 -i "${srcdir}/rpc_pipe-fix-cleanup-of-dummy-gssd-directory-when-notification-fails.patch"

	# patch source with ck patchset with BFS
	# fix double name in EXTRAVERSION
	sed -i -re "s/^(.EXTRAVERSION).*$/\1 = /" "${srcdir}/${_ckpatchname}"
	msg "Patching source with ck${_ckpatchversion} including bfs v0.444"
	patch -Np1 -i "${srcdir}/${_ckpatchname}"

	# patch source to enable more gcc CPU optimizatons via the make nconfig
	msg "Patching Kconfig.cpu to enable more gcc CPU optimizations"
	patch -Np1 -i "${srcdir}/${_gcc_patch}"

	# patch with BFQ IO Scheduler
	msg "Patching source with BFQ patches"
	for p in $(ls ${srcdir}/000{1,2,3}-block*.patch); do
        msg "$p"
		patch -Np1 -i "$p"
	done

	# add PaX patches
	msg "Patching source with PaX"
	patch -Np1 -i "${srcdir}/pax-linux-bfs-${pkgver}-${_paxver}.patch"

	# clean tree and copy ARCH config over
	msg "Running make mrproper to clean source tree"
	make mrproper

	if [ "${CARCH}" = "x86_64" ]; then
		cat "${srcdir}/config.x86_64" > ./.config
	else
		cat "${srcdir}/config" > ./.config
	fi

	### Optionally set tickrate to 1000 to avoid suspend issues as reported here:
	# http://ck-hack.blogspot.com/2013/09/bfs-0441-311-ck1.html?showComment=1379234249615#c4156123736313039413
	if [ -n "$_1k_HZ_ticks" ]; then
		msg "Setting tick rate to 1k..."
		sed -i -e 's/^CONFIG_HZ_300=y/# CONFIG_HZ_300 is not set/' \
			-i -e 's/^# CONFIG_HZ_1000 is not set/CONFIG_HZ_1000=y/' \
			-i -e 's/^CONFIG_HZ=300/CONFIG_HZ=1000/' .config
	fi

	### Optionally use running kernel's config
	# code originally by nous; http://aur.archlinux.org/packages.php?ID=40191
	if [ -n "$_use_current" ]; then
		if [[ -s /proc/config.gz ]]; then
			msg "Extracting config from /proc/config.gz..."
			# modprobe configs
			zcat /proc/config.gz > ./.config
		else
			warning "You kernel was not compiled with IKCONFIG_PROC!"
			warning "You cannot read the current config!"
			warning "Aborting!"
			exit
		fi
	fi

	if [ "${_kernelname}" != "" ]; then
		sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"${_kernelname}\"|g" ./.config
		sed -i "s|CONFIG_LOCALVERSION_AUTO=.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
	fi

	### Optionally disable NUMA since >99% of users have mono-socket systems.
	# For more, see: https://bugs.archlinux.org/task/31187
	if [ -n "$_NUMAdisable" ]; then
		if [ "${CARCH}" = "x86_64" ]; then
			msg "Disabling NUMA from kernel config..."
			sed -i -e 's/CONFIG_NUMA=y/# CONFIG_NUMA is not set/' \
				-i -e '/CONFIG_AMD_NUMA=y/d' \
				-i -e '/CONFIG_X86_64_ACPI_NUMA=y/d' \
				-i -e '/CONFIG_NODES_SPAN_OTHER_NODES=y/d' \
				-i -e '/# CONFIG_NUMA_EMU is not set/d' \
				-i -e '/CONFIG_NODES_SHIFT=6/d' \
				-i -e '/CONFIG_NEED_MULTIPLE_NODES=y/d' \
				-i -e '/# CONFIG_MOVABLE_NODE is not set/d' \
				-i -e '/CONFIG_USE_PERCPU_NUMA_NODE_ID=y/d' \
				-i -e '/CONFIG_ACPI_NUMA=y/d' ./.config
		fi
	fi

	### Optionally enable BFQ as the default I/O scheduler
	if [ -n "$_BFQ_enable_" ]; then
		msg "Setting BFQ as default I/O scheduler..."
		sed -i -e '/CONFIG_DEFAULT_IOSCHED/ s,cfq,bfq,' \
			-i -e s'/CONFIG_DEFAULT_CFQ=y/# CONFIG_DEFAULT_CFQ is not set\nCONFIG_DEFAULT_BFQ=y/' ./.config
	fi

	# set extraversion to pkgrel
	sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

	# don't run depmod on 'make install'. We'll do this ourselves in packaging
	sed -i '2iexit 0' scripts/depmod.sh
}

build() {
	cd "${srcdir}/${_srcname}"

	# get kernel version
	msg "Running make prepare for you to enable patched options of your choosing"
	make prepare

	### Optionally load needed modules for the make localmodconfig
	# See http://aur.archlinux.org/packages.php?ID=41689
	if [ -n "$_localmodcfg" ]; then
		msg "If you have modprobe_db installed, running it in recall mode now"
		if [ -e /usr/bin/modprobed_db ]; then
			[[ ! -x /usr/bin/sudo ]] && echo "Cannot call modprobe with sudo.  Install via pacman -S sudo and configure to work with this user." && exit 1
			sudo /usr/bin/modprobed_db recall
		fi
		msg "Running Steven Rostedt's make localmodconfig now"
		make localmodconfig
	fi

	if [ -n "$_makenconfig" ]; then
		msg "Running make nconfig"
		make nconfig
	fi

	# save configuration for later reuse
	if [ "${CARCH}" = "x86_64" ]; then
		cat .config > "${startdir}/config.x86_64.last"
	else
		cat .config > "${startdir}/config.last"
	fi

	msg "Running make bzImage and modules"
	make ${MAKEFLAGS} LOCALVERSION= bzImage modules
}

package_linux-ck-pax() {
	_Kpkgdesc="Linux Kernel and modules with the ck${_ckpatchversion} and pax patchsets featuring the Brain Fuck Scheduler v0.444 and PaX security patch."
	pkgdesc="${_Kpkgdesc}"
	depends=('linux-pax-flags' 'coreutils' 'linux-firmware' 'mkinitcpio>=0.7')
	optdepends=('crda: to set the correct wireless channels of your country' 'lirc-ck: Linux Infrared Remote Control kernel modules for linux-ck' 'nvidia-ck: nVidia drivers for linux-ck' 'nvidia-beta-ck: nVidia beta drivers for linux-ck' 'modprobed_db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig')
	provides=("linux-ck=${pkgver}" "linux-pax=${pkgver}" "linux=${pkgver}" 'kernel26-pax')
	conflicts=('kernel26-ck' 'kernel26-pax')
	replaces=('kernel26-ck' 'kernel26-pax')
	backup=("etc/mkinitcpio.d/linux-ck-pax.preset")
	install=linux-ck-pax.install
	groups=('base')

	sed -i -e "s/KERNEL_NAME='.*'/KERNEL_NAME='${_kernelname}'/" \
	    -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${pkgver}-${pkgrel}${_kernelname}'/" \
	    "${startdir}/${install}"

	cd "${srcdir}/${_srcname}"

	KARCH=x86

	# get kernel version
	_kernver="$(make LOCALVERSION= kernelrelease)"
	_basekernel=${_kernver%%-*}
	_basekernel=${_basekernel%.*}

	mkdir -p "${pkgdir}"/{lib/modules,lib/firmware,boot}
	make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}" modules_install
	cp arch/$KARCH/boot/bzImage "${pkgdir}/boot/vmlinuz-linux-ck-pax"

	# add vmlinux
	install -D -m644 vmlinux "${pkgdir}/usr/src/linux-${_kernver}/vmlinux"


	# set correct depmod command for install
	cp -f "${startdir}/${install}" "${startdir}/${install}.pkg"
	true && install=${install}.pkg

	sed \
		-e	"s/KERNEL_NAME=.*/KERNEL_NAME=-ck-pax/g" \
		-e	"s/KERNEL_VERSION=.*/KERNEL_VERSION=${_kernver}/g" \
		-i "${startdir}/${install}"

	# install mkinitcpio preset file for kernel
	install -D -m644 "${srcdir}/linux-ck-pax.preset" "${pkgdir}/etc/mkinitcpio.d/linux-ck-pax.preset"
	sed \
		-e "1s|'linux.*'|'linux-ck-pax'|" \
		-e "s|ALL_kver=.*|ALL_kver=\"/boot/vmlinuz-linux-ck-pax\"|g" \
		-e "s|default_image=.*|default_image=\"/boot/initramfs-linux-ck-pax.img\"|g" \
		-e "s|fallback_image=.*|fallback_image=\"/boot/initramfs-linux-ck-pax-fallback.img\"|g" \
		-i "${pkgdir}/etc/mkinitcpio.d/linux-ck-pax.preset"

	# remove build and source links
	rm -f "${pkgdir}"/lib/modules/${_kernver}/{source,build}
	# remove the firmware
	rm -rf "${pkgdir}/lib/firmware"
	# gzip -9 all modules to save 100MB of space
	find "${pkgdir}" -name '*.ko' -exec gzip -9 {} \;
	# make room for external modules
	ln -s "../extramodules-${_basekernel}${_kernelname:ck-pax}" "${pkgdir}/lib/modules/${_kernver}/extramodules"
	# add real version for building modules and running depmod from post_install/upgrade
	mkdir -p "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname:ck-pax}"
	echo "${_kernver}" > "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname:ck-pax}/version"

	# Now we call depmod...
	depmod -b "$pkgdir" -F System.map "$_kernver"

	# move module tree /lib -> /usr/lib
	mv "$pkgdir/lib" "$pkgdir/usr"
}

package_linux-ck-pax-headers() {
	_Hpkgdesc='Header files and scripts to build modules for linux-ck-pax.'
	pkgdesc="${_Hpkgdesc}"
	provides=("linux-ck-pax-headers=${pkgver}" "linux-pax-headers=${pkgver}" "linux-ck-headers=${pkgver}" "linux-headers=${pkgver}" 'kernel26-pax-headers' 'kernel26-ck-headers')
	conflicts=('kernel26-ck-pax-headers')
	replaces=('kernel26-ck-pax-headers')
	groups=('base')

	install -dm755 "${pkgdir}/usr/lib/modules/${_kernver}"

	cd "${pkgdir}/usr/lib/modules/${_kernver}"
	ln -sf ../../../src/linux-${_kernver} build

	cd "${srcdir}/${_srcname}"
	install -D -m644 Makefile \
		"${pkgdir}/usr/src/linux-${_kernver}/Makefile"
	install -D -m644 kernel/Makefile \
		"${pkgdir}/usr/src/linux-${_kernver}/kernel/Makefile"
	install -D -m644 .config \
		"${pkgdir}/usr/src/linux-${_kernver}/.config"

	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/include"

	for i in acpi asm-generic config crypto drm generated keys linux math-emu \
		media net pcmcia scsi sound trace uapi video xen; do
		cp -a include/${i} "${pkgdir}/usr/src/linux-${_kernver}/include/"
	done

	# copy arch includes for external modules
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/arch/x86"
	cp -a arch/x86/include "${pkgdir}/usr/src/linux-${_kernver}/arch/x86/"

	# copy files necessary for later builds, like nvidia and vmware
	cp Module.symvers "${pkgdir}/usr/src/linux-${_kernver}"
	cp -a scripts "${pkgdir}/usr/src/linux-${_kernver}"

	# add gcc plugins
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/tools/gcc"
	cp -a tools/gcc/*.so "${pkgdir}/usr/src/linux-${_kernver}/tools/gcc/"

	# fix permissions on scripts dir
	chmod og-w -R "${pkgdir}/usr/src/linux-${_kernver}/scripts"
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/.tmp_versions"

	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/arch/${KARCH}/kernel"

	cp arch/${KARCH}/Makefile "${pkgdir}/usr/src/linux-${_kernver}/arch/${KARCH}/"

	if [ "${CARCH}" = "i686" ]; then
		cp arch/${KARCH}/Makefile_32.cpu "${pkgdir}/usr/src/linux-${_kernver}/arch/${KARCH}/"
	fi

	cp arch/${KARCH}/kernel/asm-offsets.s "${pkgdir}/usr/src/linux-${_kernver}/arch/${KARCH}/kernel/"

	# add headers for lirc package
	# pci
	for i in bt8xx cx88 saa7134; do
		mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/pci/${i}"
		cp -a drivers/media/pci/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/pci/${i}"
	done
	# usb
	for i in cpia2 em28xx pwc sn9c102; do
		mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/${i}"
		cp -a drivers/media/usb/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/${i}"
	done
	# i2c
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c"
	cp drivers/media/i2c/*.h  "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/"
	for i in cx25840; do
		mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/${i}"
		cp -a drivers/media/i2c/${i}/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/${i}"
	done

	# add docbook makefile
	install -D -m644 Documentation/DocBook/Makefile \
		"${pkgdir}/usr/src/linux-${_kernver}/Documentation/DocBook/Makefile"

	# add dm headers
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/md"
	cp drivers/md/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/md"

	# add inotify.h
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/include/linux"
	cp include/linux/inotify.h "${pkgdir}/usr/src/linux-${_kernver}/include/linux/"

	# add wireless headers
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/net/mac80211/"
	cp net/mac80211/*.h "${pkgdir}/usr/src/linux-${_kernver}/net/mac80211/"

	# add dvb headers for external modules
	# in reference to:
	# http://bugs.archlinux.org/task/9912
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-core"
	cp drivers/media/dvb-core/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-core/"
	# and...
	# http://bugs.archlinux.org/task/11194
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/include/config/dvb/"
	# this line will allow the package to build if a user disables the dvb shit
	[[ -d include/config/dvb ]] && find include/config/dvb -name '*.h' -exec cp {} "${pkgdir}/usr/src/linux-${_kernver}/include/config/dvb/" \;

	# add dvb headers for http://mcentral.de/hg/~mrec/em28xx-new
	# in reference to:
	# http://bugs.archlinux.org/task/13146
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
	cp drivers/media/dvb-frontends/lgdt330x.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
	cp drivers/media/i2c/msp3400-driver.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/i2c/"

	# add dvb headers
	# in reference to:
	# http://bugs.archlinux.org/task/20402
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/dvb-usb"
	cp drivers/media/usb/dvb-usb/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/usb/dvb-usb/"
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends"
	cp drivers/media/dvb-frontends/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/dvb-frontends/"
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/tuners"
	cp drivers/media/tuners/*.h "${pkgdir}/usr/src/linux-${_kernver}/drivers/media/tuners/"

	# add xfs and shmem for aufs building
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/fs/xfs"
	mkdir -p "${pkgdir}/usr/src/linux-${_kernver}/mm"
	cp fs/xfs/xfs_sb.h "${pkgdir}/usr/src/linux-${_kernver}/fs/xfs/xfs_sb.h"

	# copy in Kconfig files
	for i in `find . -name "Kconfig*"`; do
		mkdir -p "${pkgdir}"/usr/src/linux-${_kernver}/`echo ${i} | sed 's|/Kconfig.*||'`
		cp ${i} "${pkgdir}/usr/src/linux-${_kernver}/${i}"
	done

	chown -R root.root "${pkgdir}/usr/src/linux-${_kernver}"
	find "${pkgdir}/usr/src/linux-${_kernver}" -type d -exec chmod 755 {} \;

	# strip scripts directory
	find "${pkgdir}/usr/src/linux-${_kernver}/scripts" -type f -perm -u+w 2>/dev/null | while read binary ; do
		case "$(file -bi "${binary}")" in
			*application/x-sharedlib*) # Libraries (.so)
				/usr/bin/strip ${STRIP_SHARED} "${binary}";;
			*application/x-archive*) # Libraries (.a)
				/usr/bin/strip ${STRIP_STATIC} "${binary}";;
			*application/x-executable*) # Binaries
				/usr/bin/strip ${STRIP_BINARIES} "${binary}";;
		esac
	done

	# remove unneeded architectures
	rm -rf "${pkgdir}"/usr/src/linux-${_kernver}/arch/{alpha,arc,arm,arm26,arm64,avr32,blackfin,c6x,cris,frv,h8300,hexagon,ia64,m32r,m68k,m68knommu,metag,mips,microblaze,mn10300,openrisc,parisc,powerpc,ppc,s390,score,sh,sh64,sparc,sparc64,tile,unicore32,um,v850,xtensa}
}
# Global pkgdesc and depends are here so that they will be picked up by AUR
pkgdesc="Linux Kernel and modules with the ck${_ckpatchversion} and pax patchsets featuring the Brain Fuck Scheduler v0.444 and PaX security patch."
