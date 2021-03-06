#   ************    LibreSilicon's StdCellLibrary   *******************
#
#   Organisation:   Chipforge
#                   Germany / European Union
#
#   Profile:        Chipforge focus on fine System-on-Chip Cores in
#                   Verilog HDL Code which are easy understandable and
#                   adjustable. For further information see
#                           www.chipforge.org
#                   there are projects from small cores up to PCBs, too.
#
#   File:           StdCellLib/Catalog/GNUmakefile
#
#   Purpose:        Makefile for Cell Generation with popcorn
#
#   ************    GNU Make 3.80 Source Code       ****************
#
#   ////////////////////////////////////////////////////////////////
#
#   Copyright (c)   2018, 2019 by
#                   chipforge - <popcorn@nospam.chipforge.org>
#   All rights reserved.
#
#       This Standard Cell Library is licensed under the Libre Silicon
#       public license; you can redistribute it and/or modify it under
#       the terms of the Libre Silicon public license as published by
#       the Libre Silicon alliance, either version 1 of the License, or
#       (at your option) any later version.
#
#       This design is distributed in the hope that it will be useful,
#       but WITHOUT ANY WARRANTY; without even the implied warranty of
#       MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#       See the Libre Silicon Public License for more details.
#
#   ////////////////////////////////////////////////////////////////////

#   project root directory, relative, used inside include.mk file
PRD =               ..

#   common definitions

include $(PRD)/include.mk

#   tool variables

MV ?=               mv
RM ?=               rm -f
TAR ?=              tar -zh
DATE :=             $(shell date -R --utc)

#   project settings

CELLS =

#   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
#       ATTENTION! Limit/Buffer changes will impact cell catalog.
#       Hence, strongly recommended, that you know what you're doing.
#   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

# global; max number of stacked mosfets
LIMIT ?=            4
# buffering recommended, but free to reduce
BUFFER ?=           $(LIMIT)
# hack limit for fencing expand algorithmen
LEVEL ?=            $(LIMIT)
# textual description for cell functionality
DESCR ?=            '?'

POPCORN ?=          $(TOOLSDIR)/popcorn/popcorn \
                    -l $(LEVEL) \
                    -b $(BUFFER) \
                    -D $(DESCR)

#   ----------------------------------------------------------------
#               DEFAULT TARGETS
#   ----------------------------------------------------------------

#   display help screen if no target is specified

.PHONY: help
help:
	#   ----------------------------------------------------------
	#       available targets:
	#   ----------------------------------------------------------
	#
	#   help       - print this help screen
	#   clean      - clean up all intermediate files
	#
	#   catalog    - compile *all* catalog cells (see list below)
	#   cell CELL=<cell> - compile up to dedicated catalog cell
	#
	#   ----------------------------------------------------------
	#       available cells [limit=$(LIMIT) + buffer=$(BUFFER)]:
	#   ----------------------------------------------------------
	#   $(CELLS)
	#

.PHONY: clean
clean:
	$(RM) $(CELLS)

.PHONY: header
header:
	#    _ __   ___  _ __   ___ ___  _ __ _ __
	#   | '_ \ / _ \| '_ \ / __/ _ \| '__| '_ \\
	#   | |_) | (_) | |_) | (_| (_) | |  | | | |
	#   | .__/ \___/| .__/ \___\___/|_|  |_| |_|
	#   |_|launched:|_| $(DATE)

#   ----------------------------------------------------------------
#               CELL TARGETS
#   ----------------------------------------------------------------

#   include makefile with highest number of (allowed) stacked transistors

ifeq ($(LIMIT),2)
    include stacked2_cells.mk
else
ifeq ($(LIMIT),3)
    include stacked3_cells.mk
else
ifeq ($(LIMIT),4)
    include stacked4_cells.mk
endif
endif
endif

.PHONY: catalog
catalog:    header $(CELLS)

.PHONY: cell
cell:       $(CELL)
