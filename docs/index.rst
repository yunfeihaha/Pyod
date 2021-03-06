.. pyod documentation master file, created by
   sphinx-quickstart on Sun May 27 10:56:38 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

PyOD Documentation
================================
.. image:: https://badge.fury.io/py/pyod.svg
    :target: https://badge.fury.io/py/pyod
.. image:: https://readthedocs.org/projects/pyod/badge/?version=latest
    :target: https://pyod.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation Status
.. image:: https://travis-ci.org/yzhao062/Pyod.svg?branch=master
    :target: https://travis-ci.org/yzhao062/Pyod
.. image:: https://coveralls.io/repos/github/yzhao062/Pyod/badge.svg?branch=master
    :target: https://coveralls.io/github/yzhao062/Pyod?branch=master&service=github
.. image:: https://img.shields.io/github/stars/yzhao062/Pyod.svg
    :alt: GitHub stars
    :target: https://github.com/yzhao062/Pyod
.. image:: https://img.shields.io/github/forks/yzhao062/Pyod.svg
    :alt: GitHub forks
    :target: https://github.com/yzhao062/Pyod
.. image:: https://mybinder.org/badge.svg
    :target: https://mybinder.org/v2/gh/yzhao062/Pyod/master

**Py**\ thon \ **O**\ utlier \ **D**\ etection (PyOD) is a comprehensive Python toolkit
to **identify outlying objects** in data with both unsupervised and supervised approaches.
This exciting yet challenging field is commonly referred as `Outlier Detection <https://en.wikipedia.org/wiki/Anomaly_detection>`_
or `Anomaly Detection <https://en.wikipedia.org/wiki/Anomaly_detection>`_.
The toolkit has been successfully used in various academic researches :cite:`a-zhao2018xgbod` and commercial products.
Unlike existing libraries, PyOD provides:

- **Unified and consistent APIs** across various anomaly detection algorithms for easy use.
- **Compatibility with both Python 2 and 3**. All implemented algorithms are also **scikit-learn compatible**.
- **Advanced functions**, e.g., **Outlier Ensemble Frameworks** to combine multiple detectors.
- **Detailed API Reference, Interactive Examples in Jupyter Notebooks** for better reliability.

**Key Links**:

- `View the latest codes on Github <https://github.com/yzhao062/Pyod>`_
- `Execute Interactive Jupyter Notebooks <https://mybinder.org/v2/gh/yzhao062/Pyod/master>`_
- `Anomaly Detection Resources <https://github.com/yzhao062/anomaly-detection-resources>`_


Important Functionalities
=========================
PyOD toolkit consists of three major groups of functionalities: (i) outlier
detection algorithms; (ii) outlier ensemble frameworks and (iii) outlier
detection utility functions.

**Individual Detection Algorithms**:

1. Linear Models for Outlier Detection:

  i. **PCA: Principal Component Analysis** (use the sum of
     weighted projected distances to the eigenvector hyperplane as the outlier
     scores) :cite:`a-shyu2003novel`: :class:`pyod.models.pca.PCA`
  ii. **MCD: Minimum Covariance Determinant** (use the mahalanobis distances
      as the outlier scores) :cite:`a-rousseeuw1999fast,a-hardin2004outlier`: :class:`pyod.models.mcd.MCD`
  iii. **One-Class Support Vector Machines** :cite:`a-ma2003time`: :class:`pyod.models.ocsvm.OCSVM`

2. Proximity-Based Outlier Detection Models:

  i. **LOF: Local Outlier Factor** :cite:`a-breunig2000lof`: :class:`pyod.models.lof.LOF`
  ii. **kNN: k Nearest Neighbors** (use the distance to the kth nearest
      neighbor as the outlier score) :cite:`a-ramaswamy2000efficient,a-angiulli2002fast`: :class:`pyod.models.knn.KNN`
  iii. **Average kNN** (use the average distance to k nearest neighbors as
       the outlier score): :class:`pyod.models.knn.KNN`
  iv. **Median kNN** (use the median distance to k nearest neighbors
      as the outlier score): :class:`pyod.models.knn.KNN`
  v. **HBOS: Histogram-based Outlier Score** :cite:`a-goldstein2012histogram`: :class:`pyod.models.hbos.HBOS`

3. Probabilistic Models for Outlier Detection:

  i. **ABOD: Angle-Based Outlier Detection** cite:`a-kriegel2008angle`: :class:`pyod.models.abod.ABOD`
  ii. **FastABOD: Fast Angle-Based Outlier Detection using approximation** cite:`a-kriegel2008angle`: :class:`pyod.models.abod.ABOD`

4. Outlier Ensembles and Combination Frameworks

  i. **Isolation Forest** :cite:`a-liu2008isolation,a-liu2012isolation`: :class:`pyod.models.iforest.IForest`
  ii. **Feature Bagging** :cite:`a-lazarevic2005feature`: :class:`pyod.models.feature_bagging.FeatureBagging`

**Outlier Detector/Scores Combination Frameworks**:

  1. **Feature Bagging**: build various detectors on random selected features :cite:`a-lazarevic2005feature`: :class:`pyod.models.feature_bagging.FeatureBagging`
  2. **Average** & **Weighted Average**: simply combine scores by averaging :cite:`a-aggarwal2015theoretical`: :func:`pyod.models.combination.average`
  3. **Maximization**: simply combine scores by taking the maximum across all
     base detectors :cite:`a-aggarwal2015theoretical`: :func:`pyod.models.combination.maximization`
  4. **Average of Maximum (AOM)** :cite:`a-aggarwal2015theoretical`: :func:`pyod.models.combination.aom`
  5. **Maximum of Average (MOA)** :cite:`a-aggarwal2015theoretical`: :func:`pyod.models.combination.moa`
  6. **Threshold Sum (Thresh)** :cite:`a-aggarwal2015theoretical`

**Utility Functions for Outlier Detection**, see :mod:`pyod.utils`.

  1. :func:`pyod.utils.utility.score_to_label`: converting raw outlier scores to binary labels
  2. :func:`pyod.utils.utility.precision_n_scores`: one of the popular evaluation metrics for outlier mining (precision @ rank n)
  3. :func:`pyod.utils.data.generate_data`: generate pseudo data for outlier detection experiment
  4. :func:`pyod.utils.stat_models.wpearsonr`:: weighted pearson is useful in pseudo ground truth generation

**Comparison of all implemented models** are made available below
(`Code <https://github.com/yzhao062/Pyod/blob/master/examples/compare_all_models.py>`_, `Jupyter Notebooks <https://mybinder.org/v2/gh/yzhao062/Pyod/master>`_):

For Jupyter Notebooks, please navigate to **"/notebooks/Compare All Models.ipynb"**

.. figure:: figs/ALL.png
    :alt: Comparison of all implemented models

Key APIs & Attributes
=====================

The following APIs are applicable for all detector models for easy use.

* :func:`pyod.models.base.BaseDetector.fit`: Fit detector.
* :func:`pyod.models.base.BaseDetector.fit_predict`: Fit detector and predict if a particular sample is an outlier or not.
* :func:`pyod.models.base.BaseDetector.fit_predict_evaluate`: Fit, predict and then evaluate with predefined metrics (ROC and precision @ rank n).
* :func:`pyod.models.base.BaseDetector.decision_function`: Predict anomaly score of X of the base classifiers.
* :func:`pyod.models.base.BaseDetector.predict`: Predict if a particular sample is an outlier or not. The model must be fitted first.
* :func:`pyod.models.base.BaseDetector.predict_proba`: Predict the probability of a sample being outlier. The model must be fitted first.

Key Attributes of a fitted model:

* :attr:`pyod.models.base.BaseDetector.decision_scores_`: The outlier scores of the training data. The higher, the more abnormal.
  Outliers tend to have higher scores.
* :attr:`pyod.models.base.BaseDetector.labels_`: The binary labels of the training data. 0 stands for inliers and 1 for outliers/anomalies.

Contents
========

.. toctree::
   :maxdepth: 2

   install
   example
   api_cc
   pyod

Quick Links
===========

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

.. rubric:: References

.. bibliography:: zreferences.bib
   :cited:
   :labelprefix: A
   :keyprefix: a-