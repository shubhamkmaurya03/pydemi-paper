# pydemi 0.2.0 paper

`main.tex`, `SI.tex` (preamble as supplied; compile with `tectonic main.tex` or pdflatex + bibtex),
`references.bib`, `figures/`, `tables/` (generated). The 0.1.0 paper is in `old_project/paper/`.

Regenerate every number, table and figure (env `pydemi`, `PYTHONPATH=src`, from the repo root):

```bash
OMP_NUM_THREADS=1 nice -n 19 python paper/analysis/ml_descriptors.py  # 56 descriptors of the 605 predicted test densities (~15 min, 16 workers)
python paper/analysis/ml_compare.py    # DFT vs predicted descriptors; properties from both  -> analysis/out/
python paper/analysis/figures.py       # figures/*.pdf, analysis/out/numbers.txt
python paper/analysis/tables.py        # tables/*.tex
python paper/analysis/gui/shots.py ~/pydemi_check/MgO_225_DFT_CHGCAR.gz paper/analysis/gui/MgO   # needs pydemi gui on :8602
```

Inputs: `property_prediction/` (descriptors, targets, study_v1 results), the stored ChargE3Net
predictions in `~/charge3net/charge3net/data/test_set_predictions_finetune/cubes`, and the 0.1.0
stability analyses in `old_project/paper/analysis/out` (valid for 0.2.0: the 56 descriptors are
identical to the 0.1.0 values on all 6,059 structures, checked in `figures.py`).
