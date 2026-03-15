# Project Context for Claude

## Project Overview

This is **Practical scRNAseq Analysis with R** - a comprehensive, reproducible bookdown course teaching single-cell RNA-seq analysis using R. The course is designed for students to execute code interactively while learning.

**Author**: Ming Tommy Tang
**Repository**: https://github.com/crazyhottommy/practical_scRNAseq_analysis_with_R
**Book URL**: https://crazyhottommy.github.io/practical_scRNAseq_analysis_with_R/

## Course Structure

This is a **bookdown** project with 5 main chapters:

1. **Chapter 1** (`01-data-download-quantification.Rmd`) - Download and quantify scRNAseq data using simpleaf/alevin-fry
2. **Chapter 2** (`02-quality-control.Rmd`) - QC and empty droplet removal with DropletUtils
3. **Chapter 3** (`03-seurat-workflow-explained.Rmd`) - Complete Seurat workflow (normalization, integration, clustering, UMAP)
4. **Chapter 4** (`04-cell-annotation.Rmd`) - Cell type annotation (SingleR, clustifyr, label transfer)
5. **Chapter 5** (`05-gene-set-enrichment.Rmd`) - GSEA with clusterProfiler
6. **Chapter 6** (`06-references.Rmd`) - Bibliography

**Dataset**: Human PBMC data from GSE126030 (Simoni et al. 2019) - 4 samples, 10x Genomics 3' v2, resting vs activated T cells

## Reproducibility Strategy

This project uses **renv** for R package version management:

- **renv.lock** - Package versions manifest (MUST be committed to git)
- **renv/activate.R** - renv infrastructure (MUST be committed)
- **renv/library/** - Package cache (excluded from git via .gitignore)

**Data Management**:
- Large data files (5.4GB total) are hosted on **Zenodo** (not in git)
- Students download via `scripts/download_data.R`
- Data folder contains: genome.fa (2.9GB), genes.gtf (1.3GB), quantification outputs, pre-processed Seurat objects

## Key Configuration Files

- **DESCRIPTION** - Package metadata with ~40+ dependencies (Seurat, SingleR, DropletUtils, clusterProfiler, etc.)
- **_bookdown.yml** - Book structure, chapter order, book filename
- **_output.yml** - Output formats (gitbook, PDF, EPUB)
- **index.Rmd** - Book introduction, prerequisites, setup, auto-generates packages.bib
- **.gitignore** - Excludes data files, renv cache, bookdown outputs

## Important Directories

```
practical_scRNAseq_analysis_with_R/
├── index.Rmd                    # Book entry point
├── 01-05-*.Rmd                  # Chapter files
├── data/                        # Data files (5.4GB, not in git)
├── results/                     # Analysis outputs (excluded from git)
├── images/                      # Figures for book
├── scripts/
│   └── download_data.R          # Zenodo data download script
├── _bookdown.yml                # Book config
├── _output.yml                  # Output formats
├── DESCRIPTION                  # Package metadata
├── renv.lock                    # Package versions (critical!)
├── .Rprofile                    # Activates renv
└── _book/                       # Rendered output (excluded from git)
```

## Development Workflow

### For Course Author (Ming):

1. **Adding/modifying chapters**:
   - Edit Rmd files in RStudio
   - Run chunks interactively for testing
   - Preview: `bookdown::preview_chapter("02-quality-control.Rmd")`
   - Full build: `bookdown::render_book("index.Rmd")`

2. **When adding new packages**:
   ```r
   BiocManager::install("newPackage")
   renv::snapshot()  # Update renv.lock
   ```

3. **Check package status**:
   ```r
   renv::status()  # Shows if new packages need to be captured
   ```

4. **Before committing**:
   - Run `renv::snapshot()` if packages changed
   - Test book build
   - Commit renv.lock along with code changes

### For Students:

1. Clone repo
2. `renv::restore()` to install packages (30-60 min)
3. `source("scripts/download_data.R")` to get data
4. Work through chapters interactively in RStudio

## Technology Stack

**R Packages** (~100+ total):
- **Single-cell analysis**: Seurat, SingleCellExperiment, scCustomize
- **Quantification**: alevinQC, fishpond
- **QC**: DropletUtils, scDblFinder, celda
- **Annotation**: SingleR, celldex, clustifyr, clustifyrdatahub
- **Integration**: harmony
- **Functional analysis**: clusterProfiler, enrichplot, msigdbr, escape
- **Visualization**: ComplexHeatmap, ggplot2
- **Utilities**: here, tidyverse (dplyr, purrr, tidyr, tibble, stringr)
- **Infrastructure**: bookdown, knitr, rmarkdown, renv

**External Tools** (mentioned in Chapter 1):
- simpleaf/alevin-fry for quantification
- fastq-dl for data download

## Status & Notes

**Current State** (as of February 2026 - Major Content Refinement Complete):

**Infrastructure** (Complete):
- All configuration files updated for reproducibility
- DESCRIPTION with full package list (~40+ dependencies)
- Bookdown config cleaned up (removed bookdown-demo references)
- index.Rmd with comprehensive prerequisites
- .gitignore configured for data exclusion and renv
- README.md with student setup instructions
- STUDENT_SETUP.md with quick start guide
- scripts/download_data.R created (needs actual Zenodo DOI)

**Content Refinement** (Complete):
- All 5 chapters comprehensively enhanced with:
  - Conceptual introductions ("why" before "how")
  - Best Practice callouts from sc-best-practices.org and OSCA
  - Common Pitfalls sections
  - Key Takeaways summaries
  - Further Reading with links to official docs and papers
  - Session info blocks for reproducibility
  - Functional programming examples with purrr
  - All emojis removed from content

**Chapter-Specific Enhancements**:

**Chapter 1 - Data Download & Quantification**:
- Added comprehensive conceptual introduction (scRNA-seq fundamentals, UMIs, cell barcodes, sparse matrices)
- Created tool landscape comparison (alevin-fry vs Cell Ranger vs kallisto vs STARsolo)
- **Critical addition**: "But Do You Really Need Single-Cell RNA-seq?" section - explains when bulk RNA-seq is better
- Cost reality check table (2024 estimates: bulk vs single-cell)
- Replication vs resolution trade-offs
- Troubleshooting section for 6 common problems
- Enhanced with splici index explanation

**Chapter 2 - Quality Control**:
- Added "The Art of Quality Control" philosophy section (permissive filtering, joint evaluation)
- Enhanced knee plot explanation with biological interpretation
- Added MAD-based thresholding section (adaptive vs fixed thresholds)
- Enhanced purrr/functional programming explanation ("Do Not Repeat Yourself" principle)
- Demonstrated walk2() vs map2(), safely() error handling
- Tissue-specific QC considerations (naive T cells, plasma B cells)

**Chapter 3 - Seurat Workflow Explained**:
- Created comprehensive 10-step pipeline overview with visual diagram
- Added "curse of dimensionality" explanation for PCA/UMAP
- Explained integration with Harmony (when to use, alternatives)
- Extensive parameter selection guidance (resolution, PCs, normalization methods)
- Enhanced normalization math with context before/after formulas
- Compared normalization methods (LogNormalize vs SCTransform vs scran) with decision tree
- Enhanced differential expression section (Wilcoxon vs presto vs pseudo-bulk approaches)
- Explained log2FC calculation differences (Seurat vs Scanpy formulas)

**Chapter 4 - Cell Annotation**:
- Added "No Ground Truth" philosophy section
- Created manual annotation workflow with marker dictionaries
- Added "Choosing a Reference Dataset" section with quality criteria table
- Explained SingleR algorithm details (Spearman correlation, 80th percentile scoring)
- Comprehensive method comparison section with consensus annotation approach
- Reference database comparison (celldex collections)
- Recommendations by scenario table

**Chapter 5 - Gene Set Enrichment Analysis**:
- Completed conceptual introduction (what is GSEA, why gene sets)
- Added 3-step GSEA algorithm walkthrough with ranking metric formula
- Gene set resources section (MSigDB collections comparison)
- Enhanced nested dataframe/purrr explanation with "Do Not Repeat Yourself" context
- Interpretation guidance (NES, FDR, effect sizes, leading edge genes)
- Added UCell signature scoring for per-cell pathway activity
- Pseudo-bulk GSEA approach mentioned

**Teaching Style Integration**:

All chapters now incorporate author's teaching philosophy from divingintogeneticsandgenomics.com:
- **Progressive complexity**: Simple examples → add complexity → biological connection
- **Problem-first, solution-second**: Explain "why" before "how"
- **purrr/functional programming**: Demonstrated as practical solutions (not academic exercises)
- **Visual thinking**: Explained plots and visualizations conceptually before showing code
- **"Do Not Repeat Yourself"**: Motivated through maintenance benefits
- **Trust but verify**: Encouraged validation and cross-checking
- **Biological grounding**: Connected computational methods to research questions
- **Casual yet authoritative tone**: Accessible but rigorous

**Technical Accuracy** (2024+ Best Practices):
- Cited sc-best-practices.org throughout (specific chapter references)
- Referenced OSCA book for statistical methods
- Included recent benchmarking papers
- Updated with 2024/2025 tool recommendations

**Remaining Tasks**:
- Initialize renv and create renv.lock (author needs to run in RStudio)
- Upload data to Zenodo and update download_data.R with actual DOI
- Test reproducibility on fresh machine
- Optional: Add cross-references between chapters using bookdown syntax

## Important Conventions

1. **File paths**: Always use `here()` package for cross-platform compatibility
2. **Caching**: Large computations use `cache=TRUE` and `cache.lazy=FALSE` in chunk options
3. **Code style**: Tidyverse conventions, pipe operator (`%>%`)
4. **Chapter independence**: Save intermediate objects (e.g., `pbmc_seurat_obj.rds`) so students can start at any chapter
5. **Git workflow**: Commit code changes + renv.lock together; never commit data files

## Common Tasks

**Render the book**:
```r
bookdown::render_book("index.Rmd", "bookdown::gitbook")
```

**Preview single chapter**:
```r
bookdown::preview_chapter("03-seurat-workflow-explained.Rmd")
```

**Clean and rebuild**:
```r
bookdown::clean_book()
bookdown::render_book("index.Rmd")
```

**Update package bibliography**:
```r
# This happens automatically in index.Rmd setup chunk
knitr::write_bib(c(.packages(), 'Seurat', 'SingleR', ...), 'packages.bib')
```

**Check renv status**:
```r
renv::status()    # What changed?
renv::snapshot()  # Update renv.lock
renv::restore()   # Install from renv.lock
```

## Things to NEVER Do

- DO NOT commit large data files (*.fa, *.gtf, *.rds) to git
- DO NOT edit renv.lock manually
- DO NOT commit renv/library/ (package cache)
- DO NOT use absolute file paths (use `here()` instead)
- DO NOT run `renv::init()` again (only do once)
- DO NOT add emojis to Rmd files (author preference)
- DO NOT modify teaching style/structure without consulting plan

## Things to ALWAYS Do

- ALWAYS use `here()` for file paths
- ALWAYS commit renv.lock when packages change
- ALWAYS test book builds before major commits
- ALWAYS keep chapters modular and independently runnable
- ALWAYS save intermediate results for student convenience
- ALWAYS maintain "why before how" teaching approach
- ALWAYS cite sources for best practices (sc-best-practices.org, OSCA)
- ALWAYS include Common Pitfalls and Key Takeaways sections

## Comprehensive Strategy Plan

A detailed implementation plan exists at `/Users/tommytang/.claude/plans/twinkling-scribbling-peacock.md` covering:

**Part A: Reproducibility Setup** (mostly complete):
- renv configuration for package management
- Zenodo data hosting strategy
- .gitignore configuration
- Documentation (README, STUDENT_SETUP)

**Part B: Content Refinement** (COMPLETE as of Feb 2026):
- Chapter-by-chapter enhancement plan
- Teaching style integration from author's blog
- Best practices incorporation from sc-best-practices.org and OSCA
- Cross-cutting improvements (callouts, pitfalls, summaries)
- Implementation priorities and verification checklists

The plan includes detailed specifications for:
- What to add to each chapter
- Code examples to enhance
- Teaching patterns to follow
- Technical accuracy sources
- Verification criteria

**All planned content enhancements have been completed.**

## Key Content Patterns

**Every chapter now includes:**
1. Conceptual introduction explaining "why" before "how"
2. At least one purrr/tidyverse teaching example
3. "Best Practice (2024)" callouts with sources
4. Interpretation guidance for results
5. "Common Pitfalls" warnings
6. "Key Takeaways" summary
7. "Further Reading" links (official docs, best practices, key papers)
8. Session info block for reproducibility

**Teaching Philosophy Applied:**
- Start with problem before solution
- Use progressive complexity (simple → complex)
- Show visual comparisons where applicable
- Connect to biological meaning
- Use functional programming naturally
- Include practical tips ("trust but verify")
- Provide specific, actionable takeaways
- Maintain casual but authoritative tone

## Important Notes for Future Sessions

**Content is Production-Ready**:
- All chapters have been comprehensively refined
- No emojis in any Rmd files (removed per author request)
- Technical accuracy vetted against 2024+ best practices
- Teaching style consistently applied throughout

**If Asked to Modify Content**:
- Maintain the established teaching style and structure
- Keep the "why before how" approach
- Preserve Best Practice callouts with sources
- Don't add emojis back
- Use purrr/tidyverse patterns where applicable

**Current Line Counts**:
- 01-data-download-quantification.Rmd: 1,213 lines
- 02-quality-control.Rmd: 738 lines
- 03-seurat-workflow-explained.Rmd: 1,286 lines
- 04-cell-annotation.Rmd: 972 lines
- 05-gene-set-enrichment.Rmd: 680 lines

**Known Placeholders to Update**:
- Zenodo DOI in scripts/download_data.R (line 16: "XXXXXXX")
- Any YouTube video links marked as "xxx"

## Contact & Resources

- **Issues**: https://github.com/crazyhottommy/practical_scRNAseq_analysis_with_R/issues
- **Strategy Plan**: `/Users/tommytang/.claude/plans/twinkling-scribbling-peacock.md`
- **Student Setup**: See STUDENT_SETUP.md for quick start guide
- **Full Documentation**: See README.md
- **Author's Blog**: https://divingintogeneticsandgenomics.com/

## License

CC BY-NC-SA 4.0 - Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International

---

**Last Updated**: 2026-02-24
**Project Phase**: Content refinement COMPLETE - all 5 chapters comprehensively enhanced with teaching philosophy, best practices, and technical accuracy. Infrastructure complete. Ready for renv initialization and Zenodo data upload.
