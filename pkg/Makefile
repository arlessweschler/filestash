VERSION=0.5
ARCH=amd64

deb:
# COPY BUILD ARTIFACT
	@echo "> Copy the build artifact"
	@[ -d filestash_$(VERSION)_$(ARCH)/usr/local/bin/filestash ] || mkdir -p filestash_$(VERSION)_$(ARCH)/usr/local/bin/filestash || true
	@cp -R ../dist/* filestash_$(VERSION)_$(ARCH)/usr/local/bin/filestash
# GENERATE DEBIAN CONTROL
	@echo "> Generating debian manifest"
	@[ -d filestash_$(VERSION)_$(ARCH)/DEBIAN ] || mkdir -p filestash_$(VERSION)_$(ARCH)/DEBIAN
	@echo "Package: Filestash" > filestash_$(VERSION)_$(ARCH)/DEBIAN/control
	@echo "Version: 0.5.20210629" >> filestash_$(VERSION)_$(ARCH)/DEBIAN/control
	@echo "Architecture: amd64" >> filestash_$(VERSION)_$(ARCH)/DEBIAN/control
	@echo "Depends: libvips, emacs, poppler-utils" >> filestash_$(VERSION)_$(ARCH)/DEBIAN/control
	@echo "Maintainer: Mickael Kerjean <mickael@kerjean.me>" >> filestash_$(VERSION)_$(ARCH)/DEBIAN/control
	@echo "Description: a web client with a pluggable backend" >> filestash_$(VERSION)_$(ARCH)/DEBIAN/control
# GENERATE SYSTEMCTL
	@echo "> Generating systemd config"
	@[ -d filestash_$(VERSION)_$(ARCH)/lib/systemd/system/ ] || mkdir -p filestash_$(VERSION)_$(ARCH)/lib/systemd/system/ || true
	@echo "[Unit]" > filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "Description=Filestash" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "After=network.target" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "[Service]" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "Type=simple" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "Restart=on-failure" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "ExecStart=/usr/local/bin/filestash/filestash" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "[Install]" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
	@echo "WantedBy=default.target" >> filestash_$(VERSION)_$(ARCH)/lib/systemd/system/filestash.service
# GENERATE THE ACTUAL DEB PACKAGE
	@echo "> Creating the DEB"
	@dpkg-deb --build --root-owner-group filestash_$(VERSION)_$(ARCH)
# Checksum
	@echo -n "MD5: "
	@cat filestash_$(VERSION)_$(ARCH).deb | md5sum
	@echo -n "SHA256: "
	@cat filestash_$(VERSION)_$(ARCH).deb | sha256sum

clean:
	@rm -rf filestash_$(VERSION)_$(ARCH)
	@rm filestash_$(VERSION)_$(ARCH).deb
