[![Python package](https://github.com/demidenm/PyReliMRI/actions/workflows/python-package-conda.yml/badge.svg?style=plastic&logo=Python)](https://github.com/demidenm/PyReliMRI/actions/workflows/python-package-conda.yml) 

[![Documentation Status](https://readthedocs.org/projects/pyrelimri/badge/?version=latest&style=plastic)](https://pyrelimri.readthedocs.io/en/latest/?badge=latest&style=plastic)
[![Funded By](https://img.shields.io/badge/NIDA-F32%20DA055334--01A1-yellowgreen?style=plastic)](https://reporter.nih.gov/project-details/10525501)
[![DOI](https://zenodo.org/badge/576430868.svg)](https://zenodo.org/badge/latestdoi/576430868)

# Python-based Reliability in MRI (PyReliMRI)

PyReliMRI is described and used in the [TBD Preprint](https://www.doi.org)

![PyReliMRI Features](/docs/img_png/pyrelimri_fig.png)
## Authors

[Michael I. Demidenko](https://orcid.org/0000-0001-9270-0124) & [Russell A. Poldrack](https://orcid.org/0000-0001-6755-0259)

### Citation

If you use PyReliMRI in your research, please cite the following Zenodo DOI:
Demidenko, M. I., & Poldrack, R. A. (2023). PyReliMRI: An Open-source Python tool for Estimates of Reliability in MRI Data [Computer software]. https://zenodo.org/record/8387971

## Intro of Problem

Reliability questions for [task fMRI](https://www.doi.org/10.1177/0956797620916786) and [resting state fMRI](https://www.doi.org/10.1016/j.neuroimage.2019.116157) are increasing. As described in [2010](https://www.doi.org/10.1111/j.1749-6632.2010.05446.x), there are various ways that researchers calculate reliability. Few open-source packages exist to calculate multiple individual and group reliability metrics using one tool.

## Purpose of Script

The purpose of this package is to provide an open-source python package that will provide multiple reliability metrics, at the group and individual level, that researchers may use to report in their manuscripts in cases of multi-run and/or multi-session data.
 - At the group level, [similarity.py](/pyrelimri/similarity.py) calculates a similarity calculations between two fMRI images using Dice or Jaccard similarity coefficients, or tetrachoric or spearman rank correlation. In addition to calculate the similarity between two images, a function is provided to pairwise comparisons across a list of 3D images and return a list of coefficients.
 - At the individual level, the [brain_icc.py](/pyrelimri/brain_icc.py) calculates voxel-wise and atlas based (see [Nilearn deterministic/probabilistic atlases](https://nilearn.github.io/dev/modules/datasets.html#atlases)) ICC(1), ICC(2,1) or ICC(3,1). For description of different ICCs and their calculations, see discussion in [Liljequist et al., 2019](https://www.doi.org/10.1371/journal.pone.0219854).


| **Script Name**                                                          | **Functions**                                                      | **Inputs**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | **Purpose**                                                                                                                                                                                                                         |
|:-------------------------------------------------------------------------|:-------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [brain_icc.py](/pyrelimri/brain_icc.py)                                  | voxelwise_icc, roi_icc                                             | [VOXELWISE_ICC] REQUIRED:<br>List of list of paths to 3D Nifti for 1+ sessions data,<br>brain mask<br>OPTIONAL:<br>ICC type (icc_type; default = 'icc_3', options include: 'icc_3','icc_2','icc_1') [ROI_ICC] REQUIRED:<br>List of list of paths to 3D Nifti for 1+ sessions data,<br>type_atlas, atlas_dir, atlas specific variables via kwargs** <br>OPTIONAL:<br> ICC type (icc_type; default = 'icc_3', options include: 'icc_3','icc_2','icc_1') | Calculate the intraclass correlation (e.g., ICC(1), ICC(2,1), or ICC(3,1) for 3D volumes across 1+ sessions, returning five 3D volumes reflecting the ICC estimate, the 95% lowerbound for ICC estimate, 95% upperbound for ICC estimate, mean squared error between subjects, mean squared error within subjects. In case of ROI icc, returns atlas labels plus array five association arrays with estimates. |
| [icc.py](/pyrelimri/icc.py)                                         | sumsq_total,<br>sumsq,<br>sumsq_btwn,<br>icc_confint,<br>sumsq_icc | REQUIRED:<br>Panda long dataframe with a subject variable (sub_var),<br>session variable (sess_var),<br>the scores (value_var) and the icc type (icc_type; default = 'icc_3', options include: 'icc_3','icc_2','icc_1')                                                                                                                                                                                                                                                                                              | Calculates sum of squares total, error, within and between to return an ICC estimate (e.g., ICC(1), ICC(2,1), or ICC(3,1), 95% lowerbound and 95% upperbound for ICC, mean between subject variance and mean within-subject variance |
| [similarity.py](/pyrelimri/similarity.py)                           | image_similarity,<br>pairwise_similarity                           | REQUIRED:<br>Path to 3D Nifti imgfile1,<br>Path to 3D Nifti imgfile2 <br>OPTIONAL:<br>Path to a mask,<br>threshold (thresh) on the images,<br>Type (similarity_type) of image similarity coefficient (default = 'dice', options include: 'dice', 'jaccard', 'tetrachoric', 'spearman')                                                                                                                                                                                                                               | Calculate the similarity between two images. Pairwise_similarity: across multiple image pairs calculate similarity coefficient between all possible combinations.                                                                   |
| [tetrachoric_correlation.py](/pyrelimri/tetrachoric_correlation.py) | tetrachoric_corr                                                   | REQUIRED:<br>Binary vector NDarray,<br>Binary vector NDarray                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Calculate the tetrachoric correlation between two binary vectors.                                                                                                                                                                   |
