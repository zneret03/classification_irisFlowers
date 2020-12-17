# Classification of Iris Flowers Project in Data Science 2

Classification of Iris Flowers using caret packages machine learning and other syntax in R that i have learn in Data Science 2
Learning Data Science is pretty fun for me, you will get your taste in different approach and statistical configuration in every data sets, Data science is helping people in various socioeconomic and health sectors. Therefore i realize that data and data scientist is there to help the world to become a better place. Learning Data Science in order to create better solutions for real-world problems that people may face today.

---

### Getting Started

1.  Install packages

    `install.packages('caret')`

    We may need other packages, but caret should ask us if we want to load them. If you are having problems with packages, you can install the caret packages and all packages that you might need by typing:

    `install.packages("caret", dependencies=c("Depends", "Suggests"))`

    Now, lets load the package that we are going to use in this entire project setup

    `library(caret)`

    The caret package provide a consistent interface into hundreds of machine learning algorithms and provides useful convenience methods for data visualization, data resampling, model that need for training and model comparison, among other features. It's a must have tool for machine learing projects in R.

2.  Load the Data

    `irisDataSet = read.csv("iris.csv", header=TRUE, stringsAsFactors=T)`

    **stringsAsFactors=T** to avoid random errors later on

    2.3 Create a Validation Dataset

    We need to know that the model we created is any good.

    Later, we will use statistical methods to estimate the accuracy of the models that we create on unseen data. We also want a more concrete estimate of the accuracy of the best model on unseen data by evaluating it on actual unseen data.
    That is, we are going to hold back some data that the algorithms will not get to see and we will use this data to get a second and independent idea of how accurate the best model might actually be.

    We will split the loaded dataset into two, 80% of which we will use to train our models and 20% that we will hold back as a validation dataset.

    create a list of 80% of the rows in the original dataset we can use for training
    `validation_index = createDataPartition(irisDataSet$Species, p=0.80, list=FALSE);`

    select 20% of the data for validation
    `validation = irisDataSet[-validation_index,];`

    use remaining 80% of ata to training and testing the models
    `irisDataSet = irisDataSet[validation_index,]`

3.  Summarize Dataset

    We will land into exciting part, now it is time to take a look at the data

    In this step we are going to tkae a look at the data a few different ways:

    1. Dimensions of the dataset
    2. Types of the attributes
    3. Peek at the data itself
    4. Levels of the class attribute.
    5. Breakdown of the instances in each class
    6. Statistical summary of all attributes

       3.1 Dimensions of Dataset

    We can get a quick idea of how many istances (rows) and how many attributes (columns) the data contains with the dim function

    `dim(irisDataSet)`

    The output should be `[1] 120 5` 120 instances and 5 attributes

    3.2 Types of attributes

    It is also good idea to get an idea of the types of the attributes we are getting from the datasets. They could be doubles, integers, strings, factors etc.

    Knowing the types is important as it will give you an idea of how to better summarize the data you have and the types of transforms you might need to use to prepare the data before you model it.

    `sapply(irisDataSet, class)`

    We should getting this output `sepal_lengths sepal_width petal_length petal_width Species "numeric" "numeric" "numeric" "numeric" "factor"`

    3.3 Peek at the Data

    it is also always a good idea to actually have an eyeball to your data.

    `head(irisDataSet)`

    We should getting this out put `sepal_lengths sepal_width petal_length petal_width Species 1 5.1 3.5 1.4 0.2 setosa 2 4.9 3.0 1.4 0.2 setosa 3 4.7 3.2 1.3 0.2 setosa 4 4.6 3.1 1.5 0.2 setosa 6 5.4 3.9 1.7 0.4 setosa 7 4.6 3.4 1.4 0.3 setosa`

    3.4 Levels of the Class

    The class variable is a factor. A factor is a class that has multiple class labels or levels. Lets peek into it

    `levels(irisDataSet$Species)`

    We should getting this type of output `[1] "setosa" "versicolor" "virginica"`

    This is a multi-class or a multinomial classification problem. If there were two levels, it would be a binary classification problem.

    3.5 Class Distribution

    Lets now take a look at the number of instances (row) that belong to each class. We can view this as an absolute count and as a percentage

    `percentage = prop.table(table(irisDataSet$Species)) * 100; cbind(freq=table(irisDataSet$Species), percentage=percentage)`
