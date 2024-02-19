[[DM Project]]
# KNN

## Model fit
```
clf = KNeighborsClassifier(n_neighbors=5, metric="euclidean", weights="uniform")
clf.fit(X_train_norm, y_train)
y_test_pred = clf.predict(X_test_norm)
```

## Performance Evaluation
Evaluate
1. accuracy
2. score
3. classification report
	1. precision, recall, f1-score
4. confusion matrix
5. roc curve
6. precision recall curve

```
print("Accuracy:", accuracy_score(y_test, y_test_pred))

# score: Return the mean accuracy on the given test data and labels.
# KNeighborsClassifier.score is doing (y_test_pred == y_test).sum() / len(y_test)
clf.score(X_test_norm, y_test)

```

```
print(classification_report(y_test, y_test_pred))
```

## Advanced Performance Evaluation of the estimator
These methods provide an estimate of the model's performance metrics (like accuracy, precision, recall) based on multiple rounds of training and validation.
For example
1. Repeated Holdout
2. Cross-Validation

### Cross Validation
The simplest way to use cross-validation is to call the [`cross_val_score`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_val_score.html#sklearn.model_selection.cross_val_score "sklearn.model_selection.cross_val_score") helper function on the estimator and the dataset.
Use StratifiedKFold.
## Hyperparameters tuning
Understand the parameters using estimator.get_params()

A search consists of:
- an estimator (regressor or classifier such as `sklearn.svm.SVC()`);
- a parameter space;
- a method for searching or sampling candidates;
- a cross-validation scheme;
- a [score function](https://scikit-learn.org/stable/modules/grid_search.html#gridsearch-scoring).

Search
1. Grid search.
	1. Systematically build and evaluate a model for each combination of algorithm parameters specified in a grid (`param_grid`). Provides the best set of hyperparameters for a model.
