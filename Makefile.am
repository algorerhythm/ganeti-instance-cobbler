osname=$(subst ganeti-instance-,,$(PACKAGE))

osdir=$(OS_DIR)/$(osname)
variantsdir=$(DESTDIR)$(sysconfdir)/ganeti/instance-cobbler/variants
configdir=$(DESTDIR)$(sysconfdir)/ganeti/instance-cobbler
defaultsdir=$(DESTDIR)$(sysconfdir)/default

dist_os_SCRIPTS = create export import rename gnt-cobbler.py
dist_os_DATA = ganeti_api_version variants.list
os_DATA = common.sh

dist_doc_DATA = COPYING NEWS README

EXTRA_DIST = common.sh.in defaults 
#	examples/hooks/grub \
#	examples/hooks/interfaces

do_subst = sed \
	-e 's,[@]sysconfdir[@],$(sysconfdir),g' \
	-e 's,[@]localstatedir[@],$(localstatedir),g'

common.sh: common.sh.in Makefile
	$(do_subst) < $< > $@
	chmod +x $@

install-exec-local:
	@mkdir_p@ "$(DESTDIR)$(osdir)"
	@mkdir_p@ $(variantsdir)
	touch $(variantsdir)/default.conf
	@mkdir_p@ $(defaultsdir)
	$(INSTALL_DATA) $(top_srcdir)/defaults \
	  $(defaultsdir)/ganeti-instance-cobbler
	ln -s $(configdir)/variants.list $(DESTDIR)$(osdir)/variants.list

uninstall-local:
	rm -f $(variantsdir)/default.conf
	rm -f $(defaultsdir)/ganeti-instance-cobbler

CLEANFILES = common.sh
