COMMIT_HASH=$(shell git rev-parse --short=7 HEAD)
COMMIT_MSG=$(shell git log -1 --pretty=%B)
COMMIT_AUTHOR=$(shell git log -1 --pretty=%an)
VERSION?=$(shell git show --format=%cd --date=format:'%y%m%d.%H%M' $(COMMIT_HASH) | head -n 1)-$(COMMIT_HASH)?=$(shell git show --format=%cd --date=format:'%y%m%d.%H%M' $(COMMIT_HASH) | head -n 1)-$(COMMIT_HASH)

new-branch:
	git checkout -b $(b) && \
	git push origin $(b) && \
	git branch --set-upstream-to origin/$(b) $(b)

delete-old-branches:
	git fetch --all --prune; git branch --verbose | grep ": gone]" | awk '{ print $1 }' | xargs -n 1 git branch --delete --force

cp:
	git add --all && \
	git commit -m "$(m)" && \
	git push



# versioning
# ##################################################################################################

increment-build-version:
	read LASTNUM < VERSION_CODE;	\
	NEWNUM=$$(($$LASTNUM + 1));		\
	echo "$$NEWNUM" > VERSION_CODE; \
	chmod +x ./tools/sanitize.sh;   \
	./tools/sanitize.sh;

gitsemver:
	@SUDO=$$([ $$(id -u) != 0 ] && echo sudo) && \
	$$(git semver help &>/dev/null) || (cd /tmp && $${SUDO} rm -rf git-semver && \
	if [ ! -d "git-semver" ]; then \
		git clone https://github.com/markchalloner/git-semver.git; \
	fi && \
	cd git-semver && \
	$${SUDO} ./install.sh)

latest-version:
	git semver get

next:
	git semver $(version)
