# Makefile for compiling, checking, formatting, and organizing LaTeX files

TEX_FILES = GeneralResearch PayloadTransportationResearch
PDF_DIR = PDFs
BUILD_DIR = build

# Extensions of compilation artifacts to clean up
TEMP_FILES = *.aux *.log *.out *.toc *.fls *.fdb_latexmk *.bak* *.synctex* indent.log

all: $(PDF_DIR) $(BUILD_DIR) $(TEX_FILES:%=$(PDF_DIR)/%.pdf)

$(PDF_DIR):
	mkdir -p $(PDF_DIR)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(PDF_DIR)/%.pdf: %.tex
	pdflatex -output-directory=$(BUILD_DIR) $<
	mv $(BUILD_DIR)/$*.pdf $(PDF_DIR)

clean:
	# Try to forcefully remove the build, PDFs, and all temp files
	rm -rf $(BUILD_DIR) $(PDF_DIR) $(TEMP_FILES)

# Stages for LaTeX linting and formatting checks

lacheck:
	@for file in $(TEX_FILES); do \
		echo "Running lacheck on $$file.tex"; \
		lacheck $$file.tex; \
	done

chktex:
	@for file in $(TEX_FILES); do \
		echo "Running chktex on $$file.tex"; \
		chktex $$file.tex; \
	done

format:
	@for file in $(TEX_FILES); do \
		echo "Formatting $$file.tex with latexindent"; \
		latexindent -w $$file.tex; \
	done
	# Clean up any artifacts left by formatting
	rm -f $(TEMP_FILES)

all_checks: lacheck chktex format

.PHONY: all clean lacheck chktex format all_checks

