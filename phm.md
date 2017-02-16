---
layout: page
title: phm
---

## PHM: Piecewise Helical Models for Hi-C data

Piecewise helical model (PHM) is a parsimonious, easy to interpret, and robust model for inferring three-dimensional (3D) chromosomal structure from Hi-C data. PHM takes the Hi-C contact matrix and local genomic features (restriction enzyme cutting frequencies, GC content and sequence uniqueness) as input
and produces, via MCMC computation, the posterior distribution of three-dimensional (3D)
chromosomal structure.

In Piecewise Helical Model, we assume that chromatin within a topologically associating domain exhibits a consensus spatial organization among the cell population. Additionally, it is known from geometry that any 3D curve can be uniquely determined by its local curvature and torsion. As a special case, a constant curvature and constant torsion lead to a helical curve. Analogous to the fact that any continuous function can be approximated by a constant at each point, the curvature and torsion of an arbitrary 3D curve can be approximated by piecewise constant functions. Therefore, any continuous 3D curve can be approximated by several well-connected helixes, which we refer to as a piecewise helical curve. Based on this, we further assume that chromatin folds like a piecewise helical curve in three dimension space.

## PHM Users' Manual
## PHM Source Code
## PHM Sample Input Data
## PHM Sample Output Data
