---
title: "Coursera Machine Learning Course"
author: "Student"
date: "Friday, August 22, 2014"
output: html_document
---

##Exploratory Data Analysis

Loading of the training and test data sets:

train <- read.csv("https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv", stringsAsFactors=FALSE)

test <- read.csv("https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv", stringsAsFactors=FALSE)

The test data set used for prediction only contains data rows with the variable "new_window" set to "no". Hence all rows in the training set containing "new_window"="yes" were deleted. The resulting training set contained 19.216 rows (observations).

train <- subset(train, train$new_window=="no")

Many variables that did not show any practical significance were elimated: X, user_name, new_window, timestamps, etc.

Using the following command, all columns that contain only empty values were removed:

train2 <- Filter(function(x)!all(x==""), train)

53 variables were remaining.

##Random Forest

For this purpose, the randomForest package was used.

install.packages("randomForest")

library(randomForest)

forest <- randomForest(class ~ ., data=train2, ntree=200, nodesize=25)

p <- predict(forest, newdata = test)

All 20 values of the test set were classified correctly.

