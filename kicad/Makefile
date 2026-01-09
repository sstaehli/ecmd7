PROJECT_NAME?=ecmd7
OUTPUT_DIR?=../$(PROJECT_NAME)-out
HUGO_DIR?=../doc/hugo/static/files

kicad?="kicad"
kicad-cli?="kicad-cli"

SHELL:=bash

.PHONY: all
all: schematic_pdf render assembly_data gerbers

.PHONY: open_project
open_project:
	$(kicad) $(PROJECT_NAME).kicad_pro &

.PHONY: schematic_pdf
schematic_pdf:
	echo "Generating documentation for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/schematic/
	$(kicad-cli) sch export pdf $(PROJECT_NAME).kicad_sch \
	-o $(OUTPUT_DIR)/schematic/$(PROJECT_NAME)_schematic.pdf
	cp $(OUTPUT_DIR)/schematic/$(PROJECT_NAME)_schematic.pdf $(HUGO_DIR)/schematic.pdf

.PHONY: assembly_data
assembly_data:
	echo "Generating assembly data for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/assembly/
	$(kicad-cli) pcb export pos $(PROJECT_NAME).kicad_pcb \
		--smd-only \
		-o $(OUTPUT_DIR)/assembly/$(PROJECT_NAME)_pnp.txt
	echo "Generating assembly drawings for $(PROJECT_NAME)..."
	$(kicad-cli) pcb export pdf $(PROJECT_NAME).kicad_pcb \
		--layers F.Fab,F.Paste \
		--include-border-title \
		-o $(OUTPUT_DIR)/assembly/$(PROJECT_NAME)_assembly.pdf
	echo "Generating BOM for $(PROJECT_NAME)..."
	$(kicad-cli) sch export bom $(PROJECT_NAME).kicad_sch \
		-o $(OUTPUT_DIR)/bom/$(PROJECT_NAME)_bom.csv

.PHONY: render
render:
	echo "Generating 3D image for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/render/
	$(kicad-cli) pcb render \
		--width 1920 --height 1080 \
		--background transparent \
		--perspective \
		--rotate 315,0,350 \
		--pan 0,1,0 \
		--zoom 1.2 \
		-o $(OUTPUT_DIR)/render/$(PROJECT_NAME)_3d.png \
		$(PROJECT_NAME).kicad_pcb
	cp $(OUTPUT_DIR)/render/$(PROJECT_NAME)_3d.png  $(HUGO_DIR)/3d.png
	$(kicad-cli) pcb render \
		--width 1920 --height 1080 \
		--background transparent \
		--rotate 0,0,0 \
		--zoom 1.2 \
		-o $(OUTPUT_DIR)/render/$(PROJECT_NAME)_2d.png \
		$(PROJECT_NAME).kicad_pcb
	cp $(OUTPUT_DIR)/render/$(PROJECT_NAME)_2d.png $(HUGO_DIR)/2d.png

.PHONY: gerbers
gerbers:
	echo "Generating Gerber files for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/gerbers/
	$(kicad-cli) pcb export gerbers $(PROJECT_NAME).kicad_pcb -o $(OUTPUT_DIR)/gerbers/
	mkdir -p $(OUTPUT_DIR)/drill/
	$(kicad-cli) pcb export drill $(PROJECT_NAME).kicad_pcb -o $(OUTPUT_DIR)/drill/