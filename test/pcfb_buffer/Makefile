.PHONY: all prsim aflat clean clean_prs clean_spice clean_prsim spice

redfont=`tput setaf 1`
greenfont=`tput setaf 2`
orangefont=`tput setaf 3`
resetterm=`tput sgr0`

PRDEPS = $(wildcard *.prdep)
SPDEPS = $(wildcard *.spdep)

all: prsim

prsim: test.sim prsim.rc

aflat: test.prs

test.sim: test.prs prsim.rc
	@cat $(word 2,$^) | prsim $(word 1,$^) > $@ && :

#-include $(PRDEPS)
test.prs: test.act
	@adepend -DLAYOUT=false -DPRSIM=true -DDUT=true $< > $(subst .act,.prdep,$<)
	@aflat -DLAYOUT=false -DPRSIM=true -DDUT=true $< > $@ && : || rm -f $@	 	

layout: test.act
	prs2net -DLAYOUT=true -B -p "pchb::adder<>" test.act > layout.spi

clean: clean_prs clean_prsim

clean_prs:
	@rm -rf *.prs
	@rm -rf *.prdep
	@rm -rf *.spdep

clean_prsim:
	@rm -rf *.sim
