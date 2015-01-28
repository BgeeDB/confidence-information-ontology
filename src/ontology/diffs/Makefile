
PERL_DIR:= ../../../tools/reporting/
OBO=http://purl.obolibrary.org/obo
ONT = confidence_information_ontology
SRC = ../$(ONT).obo
LAST = https://raw.githubusercontent.com/BgeeDB/confidence-information-ontology/master/src/ontology/$(ONT).obo

all: $(ONT)-obo-diff.html $(ONT)-def-diff.html $(ONT)-lastbuild.obo $(ONT)-combined-diff.txt

$(ONT)-obo-diff.html: $(ONT)-lastbuild.obo $(SRC)
	perl $(PERL_DIR)compare-obo-files.pl --config 'html/ontology_name=$(ONT)' --rss-path . -f1 $< -f2 $(SRC) -m html text rss -o $(ONT)-obo-diff && $(PERL_DIR)replace-amigo-urls-with-purls.pl $@
$(ONT)-def-diff.html: $(ONT)-lastbuild.obo $(SRC)
	perl $(PERL_DIR)compare-defs.pl --config 'html/ontology_name=$(ONT)' --rss-path . -f1 $< -f2 $(SRC) -m html text rss -o $(ONT)-def-diff && $(PERL_DIR)replace-amigo-urls-with-purls.pl $@

$(ONT)-combined-diff.txt: $(ONT)-def-diff.html $(ONT)-obo-diff.html
	cat $(ONT)-def-diff.txt $(ONT)-obo-diff.txt > $@

$(ONT)-lastbuild.obo: $(SRC)
	wget --no-check-certificate $(LAST) -O $@
