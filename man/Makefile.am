MAINTAINERCLEANFILES    = Makefile.in

dist_man_MANS		= sheep.8 collie.8

if BUILD_SHEEPFS
dist_man_MANS 		+= sheepfs.8
endif

EXTRA_DIST		= sheep.8.in collie.8.in sheepfs.8.in

sheep.8.options = $(shell ../sheep/sheep -h | \
	perl -ne 'print ".TP\n.BI $$1 \"\\fR, \\fP\" $$2\n$$3\n" if /^  ([^,]+), (\S+)\s+(.+)/' | \
	sed 's/\\/\\\\\\/g' | \
	sed 's/"/\\"/g' | \
	perl -pe 's/\n/\\n/g')

collie.8.options = $(shell ../collie/collie -h | \
	perl -ne 'if (/^  (.+?)  \s+(.+)/) {system "../collie/collie $$1 -h"; print "Description:\n  $$2\n"}'| \
	sed 's/Usage: collie \(.*\)/.TP\n.BI "\1"/g' | \
	sed 's/\(^[a-zA-Z]*:\)/\n\1/g' | \
	sed 's/\\/\\\\\\/g' | \
	sed 's/"/\\"/g' | \
	perl -pe 's/\n/\\n/g')

sheepfs.8.options = $(shell ../sheepfs/sheepfs -h | \
	perl -ne 'print ".TP\n.BI $$1 \"\\fR, \\fP\" $$2\n$$3\n" if /^  ([^,]+), (\S+)\s+(.+)/' | \
	sed 's/\\/\\\\\\/g' | \
	sed 's/"/\\"/g' | \
	perl -pe 's/\n/\\n/g')

%: %.in Makefile
	rm -f $@-t $@
	@sed \
		-e "s#@DATE@#`date '+%Y-%m-%d'`#g" \
		-e "s#@OPTIONS@#${$@.options}#g" \
		$< > $@-t
	mv $@-t $@

all-local: $(dist_man_MANS)

clean-local:
	rm -rf $(dist_man_MANS)
