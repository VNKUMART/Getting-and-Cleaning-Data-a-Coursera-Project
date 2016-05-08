##
## Project - Prework
## A) Download and Unzip data
if(!file.exists("./data")){dir.create("./data")}
fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileUrl,destfile="./data/Dataset.zip",method="auto")
unzip(zipfile="./data/Dataset.zip",exdir="./data")
##
## Get the list of files
path_rf <- file.path("./data" , "UCI HAR Dataset")
files<-list.files(path_rf, recursive=TRUE)
files
##
## Read Data from files
##
dataActvTest  <- read.table(file.path(path_rf, "test" , "Y_test.txt" ),
                            header = FALSE)
dataActvTrain <- read.table(file.path(path_rf, "train", "Y_train.txt"),
                            header = FALSE)
dataSbjTrain <- read.table(file.path(path_rf, "train", "subject_train.txt"),
                           header = FALSE)
dataSbjTest  <- read.table(file.path(path_rf, "test" , "subject_test.txt"),
                           header = FALSE)
dataFtrTest  <- read.table(file.path(path_rf, "test" , "X_test.txt" ),
                           header = FALSE)
dataFtrTrain <- read.table(file.path(path_rf, "train", "X_train.txt"),
                           header = FALSE)
##
## Properties 
str(dataActvTest)
str(dataActvTrain)
str(dataSbjTrain)
str(dataSbjTest)
str(dataFtrTest)
str(dataFtrTrain)
##
## 1. Merges the training and the test sets to create one data set
## -----------------------------------------------------------------------------
##
## Merge tables, Set Variable Names, Get the data frame by merging columns
##
## Merge tables
dataSbj <- rbind(dataSbjTrain, dataSbjTest)
dataActv<- rbind(dataActvTrain, dataActvTest)
dataFtr<- rbind(dataFtrTrain, dataFtrTest)
##
## Set Variable Names
names(dataSbj)<-c("Subject")
names(dataActv)<- c("Activity")
dataFtrNames <- read.table(file.path(path_rf, "features.txt"),head=FALSE)
names(dataFtr)<- dataFtrNames$V2
##
##Get the data by merging columns
dataCombine <- cbind(dataSbj, dataActv)
Data <- cbind(dataFtr, dataCombine)
##
## 2. Extracts only the measurements on the mean and standard deviation for
##    each measurement
## -----------------------------------------------------------------------------
##
## Mean and Standard Deviation
##
subdataFeaturesNames<-dataFtrNames$V2[grep("mean\\(\\)|std\\(\\)", 
                                           dataFtrNames$V2)]
##
## Subset the "Data" Frame, with selected Names of features
selectedNames<-c(as.character(subdataFeaturesNames), "Subject", "Activity")
Data<-subset(Data,select=selectedNames)
##
## Data frame structure
##
str(Data)
##
## 3. Uses descriptive activity names to name the activities in the data set
## -------------------------------------------------------------------------
##
## Descriptive activity Names
activityLabels <- read.table(file.path(path_rf, "activity_labels.txt"),
                             header = FALSE)
##
## By using descriptive activity names, factorize vairable activity in 
## data frame
##
Activity.ID = 1 
for (ActivityLabel in activityLabels$V2) { 
    Data$Activity <- gsub(Activity.ID, ActivityLabel, Data$Activity) 
    Activity.ID <- Activity.ID + 1 
} 
##
## Find what is in Data$Activity
##
head(Data$Activity,50)
tail(Data$Activity,50)
##
## 4. Appropriately labels the data set with descriptive variable names
## -----------------------------------------------------------------------------
##
## Substituting to have descriptive variable names
## 
names(Data)  ## Before changing variable names
##
## Substituting to have descriptive variable names
##
## "-mean"    ==> ".mean"
names(Data)<-gsub("-mean()", ".mean", names(Data))     
##
## "-std"     ==> ".std"
names(Data)<-gsub("-std()", ".std", names(Data))       
##
## "-"        ==> "."
names(Data)<-gsub("[-]", ".", names(Data))             
##
## Remove ()  ==> ""
names(Data)<-gsub("[()]", "", names(Data))             
##
## Prefix "t" ==> "time"
names(Data)<-gsub("^t", "time", names(Data))           
##
## Prefix "f" ==> "frequence"
names(Data)<-gsub("^f", "frequency", names(Data))      
##
## "Acc"      ==> "Accelerometer"
names(Data)<-gsub("Acc", "Accelerometer", names(Data)) 
##
## "Gyro"     ==> "Gyroscope"
names(Data)<-gsub("Gyro", "Gyroscope", names(Data))    
##
## "Mag"      ==> "Magnitude" 
names(Data)<-gsub("Mag", "Magnitude", names(Data))     
##
## "BodyBody" ==> "Body" 
names(Data)<-gsub("BodyBody", "Body", names(Data))     
##
names(Data)  ## After changing variable names
##
## 5. From #4 above, creates a second,independent tidy data set and ouput it
## -------------------------------------------------------------------------
##
Data2<-aggregate(. ~Subject + Activity, Data, mean)
Data2<-Data2[order(Data2$Subject,Data2$Activity),]
write.table(Data2, file = "tidydata.txt",row.name=FALSE)

