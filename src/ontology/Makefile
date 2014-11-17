
# This Makefile is for use by the cio Release Manager.
#
# requirements: Oort (http://code.google.com/p/owltools/wiki/OortIntro)
#
# To make a release, type 'make release' in this directory

OBO = http://purl.obolibrary.org/obo

initial-build: cio.obo
build: cio.obo minidiff
release: cio.obo diff

# all release files are derived from the editors version.
# we use the default Oort setup (hermit as reasoner)
cio.obo: cio-edit.obo
	ontology-release-runner $< --allow-overwrite --asserted --simple

# ----------------------------------------
# Imports
# ----------------------------------------
all_imports: imports/go_import.owl imports/pato_import.owl

imports/%_import.owl: cio-edit.obo
	owltools $< $(OBO)/$*.owl --add-imports-from-supports --extract-module -s $(OBO)/$*.owl -c --extract-mingraph  --set-ontology-id $(OBO)/go/extensions/$@ -o $@

# ----------------------------------------
# Diffs
# ----------------------------------------

# 
diff: cio.obo
	cd diffs && touch cio-diff && rm cio-*diff* && make

# Minidiff: intra-release differences
minidiff: cio.obo
	cd diffs  && touch cio-diff && rm cio-*diff* && make TGTS='html txt' SRC=../cio.obo && mail -s cio-diffs RELEASE-MANAGER@FOO.BAR < cio-combined-diff.txt

