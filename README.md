# 
# Course Project - Getting-and-Cleaning-Data-a-Coursera-Project

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

You should create one R script called run_analysis.R that does the following. 
1.Merges the training and the test sets to create one data set.
2.Extracts only the measurements on the mean and standard deviation for each measurement. 
3.Uses descriptive activity names to name the activities in the data set
4.Appropriately labels the data set with descriptive variable names. 
5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Project - Prework - Steps are as following

   A) Download and Unzip data
   B) Get the list of files
   C) Read Data from files
   D) Properties 

Project requirements:

1. Merged the training and the test sets to create one data set. Steps are as following.

   A) Merge tables, Set Variable Names, Get the data frame by merging columns
   B) Set Variable Names
   D) Get the data by merging columns

2. Extracted only the measurements on the mean and standard deviation for each measurement. Steps are as following.

   A) Mean and Standard Deviation
   C) Subset the "Data" Frame, with selected Names of features
   D) Data frame structure

3. Naming the activities in the data set. Steps are as following.

   A) Descriptive activity Names
   B) By using descriptive activity names, factorize vairable activity in data frame
   C) Find what is in Data$Activity

4. Label appropriately,  the data set with descriptive variable names: Steps are as following.

   A) Substituting to have descriptive variable names
      a) Subset "-mean"    ==> ".mean"
      b) Subset "-std"     ==> ".std"
      c) Subset "-"        ==> "."
      d) Subset  ()  ==> ""
      e) Subset Prefix "t" ==> "time"
      f) Subset Prefix "f" ==> "frequence"
      g) Subset "Acc"      ==> "Accelerometer"
      h) Subset "Gyro"     ==> "Gyroscope"
      i) Subset "Mag"      ==> "Magnitude" 
      j) Subset "BodyBody" ==> "Body" 

5. From #4 above, created a second, independent tidy data set and file name is tidydata.txt
