---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# feature importances

The following classifiers in scikit-learn have the feature_importances_ attribute:

- RandomForestClassifier ¹²
- ExtraTreesClassifier ¹
- GradientBoostingClassifier ¹
- DecisionTreeClassifier ³

I hope that helps! Let me know if you have any other questions.

Source: Conversation with Bing, 07/05/2023
(1) How to get most informative features for scikit-learn classifiers?. https://stackoverflow.com/questions/11116697/how-to-get-most-informative-features-for-scikit-learn-classifiers.
(2) Feature importances with a forest of trees — scikit-learn 1.2.2 .... https://scikit-learn.org/stable/auto_examples/ensemble/plot_forest_importances.html.
(3) sklearn.tree - scikit-learn 1.1.1 documentation. https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html.

Yes, there is an alternative to feature_importances_ called permutation_importance. It is available in scikit-learn's inspection module. It can be used as an alternative for impurity-based feature importances which can be misleading for high cardinality features (many unique values) ¹. 

I hope that helps! Let me know if you have any other questions.

Source: Conversation with Bing, 07/05/2023
(1) sklearn.tree - scikit-learn 1.1.1 documentation. https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html.
(2) sklearn.ensemble.RandomForestClassifier — scikit-learn 1.2.2 documentation. https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html.
(3) How to get most informative features for scikit-learn classifiers?. https://stackoverflow.com/questions/11116697/how-to-get-most-informative-features-for-scikit-learn-classifiers.

Certainly! Here is an example code that uses permutation_importance with the classifiers that support this:

```{code-cell}
from sklearn.datasets import make_classification
from sklearn.ensemble import RandomForestClassifier
from sklearn.inspection import permutation_importance

X, y = make_classification(random_state=0)
clf = RandomForestClassifier(random_state=0).fit(X, y)
result = permutation_importance(clf, X, y, n_repeats=10, random_state=0)

print(result.importances_mean)
```

This code uses the RandomForestClassifier estimator to fit the data and then uses permutation_importance to calculate feature importance scores ². 

I hope that helps! Let me know if you have any other questions.

Source: Conversation with Bing, 07/05/2023
(1) sklearn.inspection.permutation_importance - scikit-learn. https://scikit-learn.org/stable/modules/generated/sklearn.inspection.permutation_importance.html.
(2) How to use sklearn.inspection.permutation_importance for clustering .... https://stackoverflow.com/questions/59219819/how-to-use-sklearn-inspection-permutation-importance-for-clustering-algorithm.
(3) scikit-learn - sklearn.inspection.permutation_importance Permutation .... https://runebook.dev/en/docs/scikit_learn/modules/generated/sklearn.inspection.permutation_importance.
(4) 4.2. Permutation feature importance - scikit-learn. https://scikit-learn.org/stable/modules/permutation_importance.html.

+++

Sure! Here's an example code that plots the feature importance scores:

```{code-cell}
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.boxplot(result.importances.T,
           vert=False, labels=range(X.shape[1]))
ax.set_title("Permutation Importance of each feature")
ax.set_xlabel("Importance")
plt.show()
```

This code uses the result object from the previous example and plots the feature importance scores using matplotlib . 

I hope that helps! Let me know if you have any other questions.
