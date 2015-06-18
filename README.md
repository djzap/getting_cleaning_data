For more information about the data being analyzed in this project, see the CodeBook.md file.

**Instructions**

1. Clone this folder into local directory  
2. There is a single script to run. It is called `run_analysis.R`.   
    You can do this with the following code:  
    `source(run_analysis.R)`  

3. The tidy data will be written into the working directory as `run_analysis_data.txt`, and saved as the variable `tidy`.



**run_analysis.R script**

```
library(dplyr)
library(reshape2)

xtest <- read.table("data/X_test.txt")
ytest <- read.table("data/y_test.txt")
subtest <- read.table("data/subject_test.txt")
feat <- read.table("data/features.txt")
xtrain <- read.table("data/X_train.txt")
ytrain <- read.table("data/y_train.txt")
subtrain <- read.table("data/subject_train.txt")
labels <- read.table("data/activity_labels.txt")

xdata <- rbind(xtest, xtrain)
ydata <- rbind(ytest, ytrain)
subdata <- rbind(subtest, subtrain)

names(xdata) <- feat$V2
names(ydata) <- "activity"
names(subdata) <- "subject"

data <- cbind(xdata, subdata, ydata)

validnames <- make.names(names=names(data), unique=TRUE, allow_ = TRUE)
names(data) <- validnames

data <- select(data, contains("mean..."), contains("std..."), subject, activity)

long.data <- melt(data, id = c("subject", "activity"), 
                  variable.name = "feature.stat")

long.data$activity <- labels$V2[match(long.data$activity, labels$V1)]

#rename feature statistics
long.data$feature.stat <- gsub("mean...", "mean.", long.data$feature.stat)
long.data$feature.stat <- gsub("std...", "std.", long.data$feature.stat)

summarized <- summarise(group_by(long.data, subject, activity, feature.stat),
                        mean=mean(value))

tidy <- dcast(summarized, subject + activity ~ feature.stat)
tidy <- arrange(tidy, subject)

write.table(tidy, "run_analysis_data.txt", row.names = FALSE)`
```
