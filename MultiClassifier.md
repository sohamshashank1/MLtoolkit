# All vs All
*This runs binary classifier for every possible pair of classes and treat it as an election – whichever class gets the most votes wins. If we have three classes of data (red, blue and green) we would train one binary classifier for each pair of classes: 1) red vs. blue, 2) blue vs.green and 3) red vs. green.
* When new data point comes in, you check which side of each decision boundary it is on and see which class is most popular: If a new data point is on the green side of both the red vs. green and the blue vs. green hyperplanes then you classify it as green

# One vs All
* For each class a classifier is run that compares it to all the other classes at once. 
* For our red, green and blue classes, we would train one classifier for each of: 1) red vs. (green or blue), 2) green vs. (red or blue) and 3) blue vs. (red or green). In other words, the first classifier would predict whether a given point is more likely to be in the red class, or in one of the blue or green classes, and similarly for the second and third classifier. 
* We then choose a class for any new data point based on whichever class wins its own election. 

# Hierarchical classification
*  Firstly, we divide the n number of classes into 2 sets say A and B. 
* We then divide A into smaller sets of classes and same is done with B. 
* Then, we would train this binary classifier to determine whether a new data point is in some class in A, or in some class in B. (So, this step wouldn’t determine which class in A the data point is in, just whether or not it’s on one of them.) 
* We then train a second binary classifier to determine which of the two subsets of A a point is in, and a third classifier to determine which of the subsets of B a point is in. We continue all the way down, until we get to classifiers that distinguish individual classes. 



If we have a large number of classes, we can divide them into two sets of classes, say A and B. Then we can divide the classes in A into two smaller sets of classes, divide B into two smaller sets of classes and so on. To run our multi-class classification, we would first train a binary classifier to determine whether a new data point is in some class in A, or in some class in B. 
