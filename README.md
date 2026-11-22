# pydemi paper (pydemi 0.4.0)

`main.tex`, `SI.tex` (JCTC format, ACS `achemso` class, journal names in `references.bib` abbreviated as ACS asks; compile with `tectonic main.tex` or pdflatex + bibtex),
`references.bib`, `figures/`, `tables/` (generated).
`main_article.tex` is a compact article-format copy for printing (11 pt, 2 cm margins, single spacing,
no line numbers, about 18 pages instead of 37). It has no text of its own: it reads `main.tex`, so edit
`main.tex` only and compile `main_article.tex` (in Overleaf: Menu > Main document).

Regenerate every number, table and figure (env `pydemi`, `PYTHONPATH=src`, from the repo root):

```bash
OMP_NUM_THREADS=1 nice -n 19 python paper/analysis/ml_descriptors.py  # 54 descriptors of the 605 predicted test densities (~15 min, 16 workers)
python paper/analysis/ml_compare.py    # DFT vs predicted descriptors; properties from both  -> analysis/out/
python paper/analysis/figures.py       # figures/*.pdf, analysis/out/numbers.txt
python paper/analysis/tables.py        # tables/*.tex
python paper/analysis/gui/shots.py ~/pydemi_check/MgO_225_DFT_CHGCAR.gz paper/analysis/gui/MgO   # needs pydemi gui on :8602
```

Inputs: `property_prediction/` (descriptors, targets, `results/study_v2*` results; the stability
analyses in `property_prediction/sensitivity/results/` (`stability_table.csv`: grid 80 %, FD4, FD2;
`partitions_summary.csv`: Becke cells); the correlated-descriptor analysis in
`property_prediction/redundancy/`, see its README, gives `results/reasons.json` and `compare.csv`),
and the stored ChargE3Net predictions in
`~/charge3net/charge3net/data/test_set_predictions_finetune/cubes`. `tables.py` marks in blue
every table cell that differs from the submitted tables kept in `analysis/out/v1/tables`.
