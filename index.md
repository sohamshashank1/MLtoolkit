# Bagging vs Boosting algorithm 
These are ensemble methods which uses a combination of models to improve the classifier.
## Bagging 
- Random samples are drawn with replacement from the dataset and models are constructed iteratively. 
- Assignment to a particular class to unknown instance is done by majority voting given by the models. 

## Boosting
- In this process, a series of K classifiers are iteratively learnt and weights are assigned to each training tuple.
- Lets say, after a classifier Mi is learnt, the tuple weights are updated to built subsequent classifier Mi+1. Here attention is given to training tuple which was mis-classified by Mi. 
- The final boosted classifier combines votes of each individual classifier where the weights of each classifier votes.  

## XGBoost 
- This is advanced implementation of Boosting algorithm 
- XGB implement regularization 
- XGB implements parallel processing. Also, supports implementation on Hadoop
- XGB can handle missing values 
- XGB allow users to define custom optimization objectives and evaluation criteria.
- In XGB, we can define split upto maximum depth. But in Boosting would stop splitting a node when it encounters a negative loss in the split 
- XGB allows user to run a cross-validation at each iteration

### You may be wondering how can XGB do parallel processing when the models are built sequentially. 
This has been achieved by parallelizing split, i.e by sorting all the features globally and then scanning linearly to find the best split. 
- The concept implementation can be explored from [this](https://github.com/dmlc/xgboost) link. 



## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/sohamshashank1/MLtoolkit/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1 
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sohamshashank1/MLtoolkit/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
