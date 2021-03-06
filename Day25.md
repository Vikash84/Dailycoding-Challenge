## Day 25 of #dailycoding challenge ⬇️

After working on the #decision #trees, today we are going to work on #random #forest #classifier, so we are going to work on the same database (readingSkills) of the library "#party". and we will use this time the library "randomForest".

Random forest Classifier explication :
Random forest, like its name implies, consists of a large number of individual decision trees that operate as an ensemble. Each individual tree in the random forest spits out a class prediction and the class with the most votes becomes our model’s prediction .

Take a look at the code it's really amazing ⬇️

Next time we will work on randomForest with the library "#caret"

Happy Coding Learning !

``` r
# Install package party wich contains the database readingSKills
install.packages("party")
# Load the library
library(party)
# explore part of the database
print(head(readingSkills))

##====================Install package randomForest
install.packages("randomForest")
# Load the library
library(randomForest)
# Creation of the model (explain the nativeSpeaker variable based on the other variables)
set.seed(123)
fit <- randomForest(nativeSpeaker ~ ., data = readingSkills, na.action = na.roughfix)
print(fit)

# Classification of explanatory variables
# with a plot 
varImpPlot(fit)
# with a matrix
fit$importance
# examine graphically the importance of the variables to distinguish the variable nativespeaker
plot(nativeSpeaker ~score, data = readingSkills )
plot(nativeSpeaker ~shoeSize, data = readingSkills)
plot(nativeSpeaker ~age, data = readingSkills)

# Prediction on a new dataset
base=cbind(age=c(8,11,6),shoeSize=c(25,25,30),score=c(30,40,55))
predicted=predict(fit,newdata=base)
predicted

# improve the prediction of Random Forest
##Choice of ntree (number of trees)

set.seed(123)
fit <- randomForest(nativeSpeaker~ ., data = readingSkills , ntree = 880, 
                    , na.action = na.roughfix)
print(fit)

plot(fit$err.rate[, 1], type = "l", xlab = "nombre d'arbres", ylab = "erreur OOB" ,main="OOB en fonction du nombre d'arbres")

### Conclusion : the optimal number of trees is 880


 ##Choice of mtree (number of variables)\knowing that the number of trees is 2000
set.seed(123)
fit <- randomForest(formula = nativeSpeaker ~ ., data = readingSkills,ntree=2000, 
                    mtry = 3, na.action = na.roughfix)
print(fit)

set.seed(123)
fit <- randomForest(formula = nativeSpeaker ~ ., data = readingSkills,ntree=2000, 
                    mtry = 2, na.action = na.roughfix)
print(fit)

### Conclusion : for 2000 trees the best number of featurs is 2 (score and shoeSize )
```


