# TidydataCoursera
Coursera "Getting and Cleaning Data Course" Project  Assignment 3
#filepath automated generation
setwd("C:/Users/lerouxd/Desktop/Coursera")
fptest <- file.path(getwd(),"UCI HAR Dataset/test")
fptrain <- file.path(getwd(),"UCI HAR Dataset/train")
fpUCI<- file.path(getwd(),"UCI HAR Dataset")

#Upload  test files
setwd(fptest)
STe <- read.table("subject_test.txt")
yTe<- read.table("y_test.txt")
XTe <- read.table("X_test.txt")
setwd("C:/Users/lerouxd/Desktop/Coursera")


#upload feature names
#upload activity names
setwd(fpUCI)
FN <- read.table("features.txt",header=FALSE) [,2]
AL <- read.table("activity_labels.txt")
setwd("C:/Users/lerouxd/Desktop/Coursera")

#Upload  train files: y is "activity" - X is "features" _ S is "subject"
setwd(fptrain)
STr <- read.table("subject_train.txt")
yTr <- read.table("y_train.txt")
XTr <- read.table("X_train.txt")
setwd("C:/Users/lerouxd/Desktop/Coursera")

#Rename X files
names(XTr) = FN
names(XTe) = FN

#PART1: Merge  test & train files
S <- rbind(STr, STe)
y <- rbind(yTr, yTe)
X <- rbind(XTr, XTe)

#PART2.	Extracts only the indices or names  of mean and standard deviation for each measurement. 
# matrix tranform to allow next step "descriptive headers"
FNt=t(FN)
FNmeanstdindices<- grep("mean|std", FNt)
FNmeanstd=FNt[FNmeanstdindices]

# PART3:Naming the columns.	Uses descriptive activity to name  activities in the FULL RENAMED DATASET "FRD"

colnames(y) <- "Activity"
colnames(S) <- "Subject"
FRD <- cbind(X,y,S)

#Extract std & mean from FRD (after having renamed, it is repeatt of PART 2 but 
#I was following the instructions sequences: my choice is to (1) RENAME than to (2) BIND than (3) to extract from renamed data)

FRD_meanstd<-FRD[,FNmeanstdindices]

#PART4: Appropriately labels the data set with descriptive variable names. 

names(FRD_meanstd)<-gsub("Acc", "Accelerometer-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("Gyro", "Gyroscope-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("BodyBody", "Body-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("Mag", "Magnitude-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("^t", "Time-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("^f", "Frequency-", names(FRD_meanstd))
names(FRD_meanstd)<-gsub("tBody", "TimeBody-", names(FRD_meanstd))

#PART5
#ANSWER is TYFILE "FRD_meanstd"




