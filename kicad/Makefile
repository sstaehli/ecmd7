PROJECT_NAME?=ecmd7
OUTPUT_DIR?=../$(PROJECT_NAME)-out

kicad?="C:\Program Files\KiCad\9.0\bin\kicad.exe"
kicad-cli?="C:\Program Files\KiCad\9.0\bin\kicad-cli.exe"

SHELL:=bash

.PHONY: open_project
open_project:
	$(kicad) $(PROJECT_NAME).kicad_pro &

.PHONY: schematic_pdf
schematic_pdf:
	echo "Generating documentation for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/schematic/
	$(kicad-cli) sch export pdf $(PROJECT_NAME).kicad_sch \
	-o $(OUTPUT_DIR)/schematic/$(PROJECT_NAME)_schematic.pdf

.PHONY: assembly_data
assembly_data:
	echo "Generating assembly data for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/assembly/
	$(kicad-cli) pcb export pos $(PROJECT_NAME).kicad_pcb \
	--smd-only \
	-o $(OUTPUT_DIR)/assembly/$(PROJECT_NAME)_pnp.txt
	echo "Generating assembly drawings for $(PROJECT_NAME)..."
	$(kicad-cli) pcb export pdf $(PROJECT_NAME).kicad_pcb \
	--layers F.Fab \
	-o $(OUTPUT_DIR)/assembly/$(PROJECT_NAME)_assembly.pdf

.PHONY: gerbers
gerbers:
	echo "Generating Gerber files for $(PROJECT_NAME)..."
	mkdir -p $(OUTPUT_DIR)/gerbers/
	$(kicad-cli) pcb export gerbers $(PROJECT_NAME).kicad_pcb -o $(OUTPUT_DIR)/gerbers/
	mkdir -p $(OUTPUT_DIR)/drill/
	$(kicad-cli) pcb export drill $(PROJECT_NAME).kicad_pcb -o $(OUTPUT_DIR)/drill/