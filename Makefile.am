VERSION=0.1.0
LANG1=es
LANG2=an
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)
BASENAME=apertium-$(PREFIX1)

VAR1=std # Aragonés cheneral
VAR2=rib # Aragonés ribagorzano
VAR3=chi # Aragonés chistabín
PREFVAR1=#dejar en blanco
PREFVAR2=rib-
PREFVAR3=chi-
TARGETS_COMMON = $(PREFIX1).automorf.bin $(PREFIX1).autobil.bin $(PREFIX1).autogen.bin \
     $(PREFIX1).autopgen.bin $(PREFIX2).automorf.bin $(PREFIX2).autobil.bin \
     $(PREFIX2).autogen.bin $(PREFIX2).autopgen.bin modes 

#TARGETS = $(TARGETS_COMMON) trules-$(PREFIX1).bin trules-$(PREFIX2).bin \
#          trules-$(PREFIX1).xml trules-$(PREFIX2).xml
#

TARGETS = $(TARGETS_COMMON) trules-$(PREFIX2).bin \
          trules-$(PREFIX2).xml

.deps/commonbil.dix: $(BASENAME).$(PREFIX1).dix
	xsltproc --stringparam alt $(VAR1) alt.xsl $< >$@

.deps/$(PREFVAR1)$(LANG1).dix: $(BASENAME).$(LANG1).dix
	xsltproc --stringparam alt $(VAR1) alt.xsl $< >$@

#.deps/$(PREFVAR2)$(LANG1).dix: $(BASENAME).$(LANG1).dix
#	xsltproc --stringparam alt $(VAR2) alt.xsl $< >$@
#
#.deps/$(PREFVAR3)$(LANG1).dix: $(BASENAME).$(LANG1).dix
#	xsltproc --stringparam alt $(VAR3) alt.xsl $< >$@

.deps/$(PREFVAR1)$(LANG2).dix: $(BASENAME).$(LANG2).dix
	xsltproc --stringparam alt $(VAR1) alt.xsl $< >$@

#.deps/$(PREFVAR2)$(LANG2).dix: $(BASENAME).$(LANG2).dix
#	xsltproc --stringparam alt $(VAR2) alt.xsl $< >$@

.deps/common-$(PREFIX1).dix: $(BASENAME).$(PREFIX1).dix
	xsltproc translate-to-default-equivalent.xsl $< >$@

.deps/$(PREFVAR1)$(PREFIX1).dix: .deps/common-$(PREFIX1).dix
	xsltproc --stringparam alt $(VAR1) alt.xsl $< >$@

.deps/$(PREFVAR2)$(PREFIX1).dix: .deps/common-$(PREFIX1).dix
	xsltproc --stringparam alt $(VAR2) alt.xsl $< >$@

$(PREFVAR1)$(PREFIX1).automorf.bin: .deps/$(PREFVAR1)$(LANG1).dix $(BASENAME).$(LANG1).acx
	apertium-validate-acx $(BASENAME).$(LANG1).acx
	apertium-validate-dictionary $<
	lt-comp lr $< $@ $(BASENAME).$(LANG1).acx

$(PREFVAR1)$(PREFIX1).autobil.bin: .deps/$(PREFVAR1)$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFVAR1)$(PREFIX1).autogen.bin: .deps/$(PREFVAR1)$(LANG2).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFIX1).autopgen.bin: $(BASENAME).post-$(LANG2).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFVAR1)$(PREFIX2).automorf.bin: .deps/$(PREFVAR1)$(LANG2).dix $(BASENAME).$(LANG2).acx
	apertium-validate-acx $(BASENAME).$(LANG2).acx
	apertium-validate-dictionary $<
	lt-comp lr $< $@ $(BASENAME).$(LANG2).acx

$(PREFVAR1)$(PREFIX2).autobil.bin: .deps/$(PREFVAR1)$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFVAR1)$(PREFIX2).autogen.bin: .deps/$(PREFVAR1)$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

$(PREFVAR1)$(PREFIX2).autopgen.bin: $(BASENAME).post-$(LANG1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

#$(PREFVAR2)$(PREFIX1).automorf.bin: .deps/$(PREFVAR2)$(LANG1).dix $(BASENAME).$(LANG1).acx
#	apertium-validate-acx $(BASENAME).$(LANG1).acx
#	apertium-validate-dictionary $<
#	lt-comp lr $< $@ $(BASENAME).$(LANG1).acx
#
#$(PREFVAR2)$(PREFIX1).autobil.bin: .deps/$(PREFVAR2)$(PREFIX1).dix
#	apertium-validate-dictionary $<
#	lt-comp lr $< $@
#
#$(PREFVAR2)$(PREFIX1).autogen.bin: .deps/$(PREFVAR2)$(LANG2).dix
#	apertium-validate-dictionary $<
#	lt-comp rl $< $@
#
#$(PREFVAR2)$(PREFIX2).automorf.bin: .deps/$(PREFVAR2)$(LANG2).dix $(BASENAME).$(LANG2).acx
#	apertium-validate-acx $(BASENAME).$(LANG2).acx
#	apertium-validate-dictionary $<
#	lt-comp lr $< $@ $(BASENAME).$(LANG2).acx
#
#$(PREFVAR2)$(PREFIX2).autobil.bin: .deps/$(PREFVAR2)$(PREFIX1).dix
#	apertium-validate-dictionary $<
#	lt-comp rl $< $@
#
#$(PREFVAR2)$(PREFIX2).autogen.bin: .deps/$(PREFVAR2)$(LANG1).dix
#	apertium-validate-dictionary $<
#	lt-comp rl $< $@
#
#trules-$(PREFIX1).bin: $(BASENAME).trules-$(PREFIX1).xml
#	apertium-validate-transfer $(BASENAME).trules-$(PREFIX1).xml
#	apertium-preprocess-transfer $(BASENAME).trules-$(PREFIX1).xml \
#	                             trules-$(PREFIX1).bin

trules-$(PREFIX2).bin: $(BASENAME).trules-$(PREFIX2).xml
	apertium-validate-transfer $(BASENAME).trules-$(PREFIX2).xml
	apertium-preprocess-transfer $(BASENAME).trules-$(PREFIX2).xml \
	                             trules-$(PREFIX2).bin

#trules-$(PREFIX1).xml: $(BASENAME).trules-$(PREFIX1).xml
#	ln -s $(BASENAME).trules-$(PREFIX1).xml trules-$(PREFIX1).xml

trules-$(PREFIX2).xml: $(BASENAME).trules-$(PREFIX2).xml
	ln -s $(BASENAME).trules-$(PREFIX2).xml trules-$(PREFIX2).xml

EXTRA_DIST=$(BASENAME).$(LANG1).dix $(BASENAME).$(PREFIX1).dix \
           $(BASENAME).post-$(LANG1).dix $(BASENAME).post-$(LANG2).dix \
           $(BASENAME).$(LANG2).dix $(BASENAME).$(LANG1).tsx \
           $(BASENAME).trules-$(PREFIX2).xml $(PREFIX1).prob $(PREFIX2).prob \
           modes.xml translate-to-default-equivalent.xsl alt.xsl filter.xsl filter.sh \
           $(BASENAME).$(LANG1).acx $(BASENAME).$(LANG2).acx


apertium_es_andir=$(prefix)/share/apertium/apertium-$(PREFIX1)/
apertium_es_modesdir=$(prefix)/share/apertium/modes/

$(PREFIX1).mode: modes.xml 
	apertium-gen-modes modes.xml
	cp *.mode modes/

$(PREFIX2).mode: modes.xml 
	apertium-gen-modes modes.xml
	cp *.mode modes/

modes: modes.xml
	apertium-gen-modes modes.xml

apertium_es_an_DATA=$(PREFVAR1)$(PREFIX1).automorf.bin $(PREFVAR1)$(PREFIX2).automorf.bin \
	$(PREFVAR1)$(PREFIX1).autobil.bin $(PREFVAR1)$(PREFIX2).autobil.bin \
	$(PREFVAR1)$(PREFIX1).autogen.bin $(PREFVAR1)$(PREFIX2).autogen.bin \
	$(PREFIX1).autopgen.bin $(PREFIX2).autopgen.bin \
	$(PREFIX1).prob $(PREFIX2).prob \
	trules-$(PREFIX2).xml  \
	trules-$(PREFIX2).bin \
	$(PREFVAR1)$(PREFIX2).mode 

install-data-local:
	apertium-gen-modes modes.xml apertium-$(PREFIX1)
	cp *.mode modes/
	$(INSTALL_DATA) $(PREFVAR1)$(PREFIX2).mode $(apertium_es_modesdir)
	$(INSTALL_DATA) $(BASENAME).trules-$(PREFIX2).xml $(apertium_es_andir)

CLEANFILES = -rf $(TARGETS) modes .deps/ 

