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
dt = DecisionTreeClassifier(max_depth =6, random_state=SEED)

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
