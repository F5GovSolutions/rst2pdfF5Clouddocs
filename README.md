# rst2pdfF5Clouddocs

This repo is just this doc detailing how to take F5 Clouddocs guides and turn them into a pdf for situations such as closed networks

This guide details instructions for Ubuntu (22.04 and 24.04), it should be similar to other distros if not very close for apt based distros.
Make sure you have at least 2GB of RAM.

This will install the rst2pdf command, this requires internet access.
Commands to be executed in bold.

Ensure python3 and pip3 (python package installer) are installed

sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install python3 python3-pip
sudo apt-get -y install git



sudo pip3 install rst2pdf[aafiguresupport,mathsupport,plantumlsupport,rawhtmlsupport,sphinx,svgsupport]

pip3 install rst2pdf
pip3 install sphinxcontrib
pip3 install f5_sphinx_theme
pip3 install sphinxcontrib-blockdiag
pip3 install sphinx-copybutton
pip3 install sphinxcontrib-nwdiag
https://clouddocs.f5.com/training/community/rseries-training/html/#planning-for-rseries-guide
Find the appropriate repo here
https://github.com/f5devcentral/

For instance the rSeries training above is located here
https://github.com/f5devcentral/f5-rseries-training

git clone https://github.com/f5devcentral/f5-rseries-training

after cloning the rst repo, edit the the <repo>/docs/conf.py

add the following to the extensions = [

section

'sphinx.ext.autodoc','rst2pdf.pdfbuilder'

The resulting section should look something like

extensions = [
  'sphinx.ext.todo',
  'sphinx.ext.extlinks',
  'sphinx.ext.graphviz',
  'sphinxcontrib.nwdiag',
  'sphinx_copybutton',
  'sphinxcontrib.blockdiag',
  'sphinx.ext.autodoc',
  'rst2pdf.pdfbuilder'
  #'sphinx.ext.autosectionlabel'
]

At the very end of conf.py add the following lines

#########
# -- Options for PDF output --------------------------------------------------

# Grouping the document tree into PDF files. List of tuples
# (source start file, target name, title, author, options).
#
# If there is more than one author, separate them with \\.
# For example: r'Guido van Rossum\\Fred L. Drake, Jr., editor'
#
# The options element is a dictionary that lets you override
# this config per-document. For example:
#
# ('index', 'MyProject', 'My Project', 'Author Name', {'pdf_compressed': True})
#
# would mean that specific document would be compressed
# regardless of the global 'pdf_compressed' setting.

pdf_documents = [
    ('index', 'MyProject', 'My Project', 'Author Name'),
]

# A comma-separated list of custom stylesheets. Example:
pdf_stylesheets = ['sphinx', 'a4']

# A list of folders to search for stylesheets. Example:
pdf_style_path = ['.', '_styles']

# Create a compressed PDF
# Use True/False or 1/0
# Example: compressed=True
# pdf_compressed = False

# A colon-separated list of folders to search for fonts. Example:
# pdf_font_path = ['/usr/share/fonts', '/usr/share/texmf-dist/fonts/']

# Language to be used for hyphenation support
# pdf_language = "en_US"

# Mode for literal blocks wider than the frame. Can be
# overflow, shrink or truncate
# pdf_fit_mode = "shrink"

# Section level that forces a break page.
# For example: 1 means top-level sections start in a new page
# 0 means disabled
# pdf_break_level = 0

# When a section starts in a new page, force it to be 'even', 'odd',
# or just use 'any'
# pdf_breakside = 'any'

# Insert footnotes where they are defined instead of
# at the end.
# pdf_inline_footnotes = True

# verbosity level. 0 1 or 2
# pdf_verbosity = 0

# If false, no index is generated.
# pdf_use_index = True

# If false, no modindex is generated.
# pdf_use_modindex = True

# If false, no coverpage is generated.
# pdf_use_coverpage = True

# Name of the cover page template to use
# pdf_cover_template = 'sphinxcover.tmpl'

# Label to use as a prefix for the subtitle on the cover page
# subtitle_prefix = 'version'

# Documents to append as an appendix to all manuals.
# pdf_appendices = []

# Enable experimental feature to split table cells. Use it
# if you get "DelayedTable too big" errors
# pdf_splittables = False

# Set the default DPI for images
# pdf_default_dpi = 72

# Enable rst2pdf extension modules
# pdf_extensions = []

# Page template name for "regular" pages
# pdf_page_template = 'cutePage'

# Show Table Of Contents at the beginning?
# pdf_use_toc = True

# How many levels deep should the table of contents be?
pdf_toc_depth = 9999

# Add section number to section references
pdf_use_numbered_links = False

# Background images fitting mode
pdf_fit_background_mode = 'scale'

# Repeat table header on tables that cross a page boundary?
pdf_repeat_table_rows = True

# Enable smart quotes (1, 2 or 3) or disable by setting to 0
pdf_smartquotes = 0
######


Lastly comment out the line
#html4_writer = True


sphinx-build -b pdf f5-rseries-training/docs/  build/pdf

Be patient as this can take some time. On a 2 vcpu 2GB RAM vm, it took 20mins to create a 1k page doc.
