# DecisionTree
Machine learning algorithm that detects false banknotes in a UC Irvine dataset. Implemented in Matlab based on the decision tree and random forest descriptions in *Artificial Intelligence: A Modern Approach* 3rd Edition by Stuart Russell and Peter Norvig. The only prerequisites are Matlab itself and the parallel computing toolbox. Results are verified using K-Fold cross validation. The UC Irvine dataset is available here: https://archive.ics.uci.edu/ml/datasets/banknote+authentication.

The script main.m calls crossValidation() and crossValidationWithDeletion() after generating either inputs for a single decision tree or inputs for a random forest. The crossValidation() functions perform what their names imply by repeatedly dividing the data into different segments for training and learning, deleting attributes if appropriate, and calling the decisionTreeLearning() to generate a decision tree based on the learning data sets. The cross validation functions compute and return confusion matrices for all of the iterations in the cross validations; main.m prints the confusion matrices, precision, and recall. The decisionTreeLearning() algorithm implements the algorithm written on page 702 of the Russel and Norvig text with some modifications. First, it does not remove attributes from the attribute list before every recursive call. This is because the algorithm in the textbook was based on attributes that have only values such as true or false while this dataset has continuously valued attributes. If an attribute has only two possible values, then it makes sense to no longer consider it after each of the two values have already been considered. This does not make sense when an attribute has many values with many possible split points; the tree would be too short if attributes were removed in the continuous case. Second, the decisionTreeLearning() function is modified to follow the directions in parts (a) and (b) of this problem. It looks at the data it receives and provides data where it does not exist. The crossValidationWithDeletion() function “deletes” data by replacing it with NaN; decisionTreeLearning() simply detects NaN. The data structure used by decisionTreeLearning() to represent a tree is a nested MATLAB cell array. If the cell array contains the string ‘END_TREE’, then the function knows that that cell array represents a leaf in the tree and no more recursive calls should be made. If the cell array is not a leaf, it contains a new cell array generated by the next call of decisionTreeLearning(). Two last important functions are getHighestImportanceAttribute() and getSplitPoint(). getHighestImportanceAttribute() does what it’s title implies based on page 702, while getSplitPoint() implements the split point determining algorithm described on page 707 of Russel and Norvig.
