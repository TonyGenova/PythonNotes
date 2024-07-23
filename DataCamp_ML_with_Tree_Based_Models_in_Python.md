### Chapter 1 - Classification and Regression Trees (CART)   
Learns a sequence of if/else (true/false) questions to determine labels  
Doesn't have to be linear, can be non-linear  
Maximum depth = maximum number of branches    
Trees have decision regions and decision boundaries - this are where the splits happen  
Split data into train/test split first  
random state parameter allows reproducability  
```python
# Import DecisionTreeClassifier from sklearn.tree
from sklearn.tree import DecisionTreeClassifier

# Instantiate a DecisionTreeClassifier 'dt' with a maximum depth of 6
dt = DecisionTreeClassifier(max_depth =6, random_state=1)

# Fit dt to the training set
dt.fit(X_train, y_train)

# Predict test set labels
y_pred = dt.predict(X_test)
print(y_pred[0:5])

# Import accuracy_score
from sklearn.metrics import accuracy_score

# Predict test set labels
y_pred = dt.predict(X_test)

# Compute test set accuracy  
acc = accuracy_score(y_test, y_pred)
print("Test set accuracy: {:.2f}".format(acc))
```

#### Logistic regression vs classification tree
A classification tree divides the feature space into rectangular regions. In contrast, a linear model such as logistic regression produces only a single linear decision boundary dividing the feature space into two decision regions.
```python
# Import LogisticRegression from sklearn.linear_model
from sklearn.linear_model import  LogisticRegression

# Instatiate logreg
logreg = LogisticRegression(random_state=1)

# Fit logreg to the training set
logreg.fit(X_train, y_train)

# Define a list called clfs containing the two classifiers logreg and dt
clfs = [logreg, dt]

# Review the decision regions of the two classifiers
plot_labeled_decision_regions(X_test, y_test, clfs)
```

#### Classification Tree Learning  
Decision tree is built of three types of nodes  
 - Root Node: no parent, two children (ie start node)
 - Internal Node: has parent, two children
 - Leaf: One parent node, ends up being final prediction

##### Information Gain  
Tree maximizes information gain at each split  
Impurity of a node can be measured by gini index or entropy  

##### Building a Tree 
 - Nodes are grown recursively
 - non-leaf nodes are created to maximize information gain
 - if no information can be gained, you end at a leaf
 - assuming you aren't at max leafs yet!

#####  Using entropy as a criterion  
In this exercise, you'll train a classification tree on the Wisconsin Breast Cancer dataset using entropy as an information criterion. You'll do so using all the 30 features in the dataset, which is split into 80% train and 20% test.

X_train as well as the array of labels y_train are available in your workspace.
```python
# Import DecisionTreeClassifier from sklearn.tree
from sklearn.tree import DecisionTreeClassifier

# Instantiate dt_entropy, set 'entropy' as the information criterion
dt_entropy = DecisionTreeClassifier(max_depth=8, criterion='entropy', random_state=1)

# Fit dt_entropy to the training set
dt_entropy.fit(X_train, y_train)
```
##### Entropy vs Gini index  
In this exercise you'll compare the test set accuracy of dt_entropy to the accuracy of another tree named dt_gini. The tree dt_gini was trained on the same dataset using the same parameters except for the information criterion which was set to the gini index using the keyword 'gini'.
```python

# Import accuracy_score from sklearn.metrics
from sklearn.metrics import accuracy_score

# Use dt_entropy to predict test set labels
y_pred= dt_entropy.predict(X_test)

# Evaluate accuracy_entropy
accuracy_entropy = accuracy_score(y_test, y_pred)

# Print accuracy_entropy
print(f'Accuracy achieved by using entropy: {accuracy_entropy:.3f}')
# The code in the class never calculates this???
# Print accuracy_gini
print(f'Accuracy achieved by using the gini index: {accuracy_gini:.3f}')
```
