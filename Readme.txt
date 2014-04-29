Steps that needs to be followed to test the code

Pre-requisite:

1. hadoop file system/yarn should be running.
2. Logged in user should have permission to read/write files. Otherwise give permissions to Project2->jar->data.

Part 1.WordCount

For this question refer code in Project2->code->TweetWordCount.zip file

1. Use the collection of tweet in a single file (sample: tweets.txt present in Project2->jar->data)
2. User should have permission to write the files in current folder. If not, Please give the permissions to following folders
   Project2->jar->data. Change the current directory to Project2->jar. Now run the file CleanTweets.jar using "java -jar TweetWordCount.jar TweetProcessing.CleanTweets" and you will get the required clean tweet file ie cleanFile.txt in Project2->jar->data.
3.Now run wordcount program given by professor on the cleanFile.txt using below steps
	
	a.Please make your current directory as Project2->jar->data
	b.hdfs dfs -rmr /input/* 	(to remove all the existing files in input folder)
	c.hdfs dfs -mkdir /input 	(if input folder doesn't exist)
	d.move the cleanFile.txt from Project2->jar->data to /input use below cmd
	e.hdfs dfs -copyFromLocal cleanFile.txt /input
	f.Now come out of data folder using cd ..
	g.hadoop jar wordcount-sample.jar sample.WordCount(access the wordcount-sample.jar file from Project2->data->jar)

4.Now we have the total count of all the words in our tweets. You can access the output file from /output
5.Copy the file to local and sort the file obtained by using below cmd
	a.hdfs dfs -copyToLocal /output/part-r-00000
	b.sort -k2nr part-r-00000 > data/cleanWcSort.txt
	c.now we have the output in cleanWcSort file

6.Now run the TopResult.jar from Project2->jar folder using below cmd
	java -jar TopResults.jar TweetProcessing.topTagUsersTrend
  ouptput->we will get 3 files hashTags.txt, users.txt, trends.txt in the data folder which gives the top hashtags,users and trends


	
Part2.a Pairs

For this question refer code in Project2->code->Pairs.zip file. 

1.Copy the cleanFile.txt from Project2->jar->data and put in pairsInput folder using below cmd
	
	a.Please make your current directory as Project2->jar->data
	b.hdfs dfs -rm /pairsInput/* 	(to remove all the existing files in input folder)
	c.hdfs dfs -mkdir /pairsInput 	(if input folder doesn't exist)
	d.move the cleanFile.txt from Project2->jar->data to /pairsInput using below cmd
	e.hdfs dfs -copyFromLocal cleanFile.txt /pairsInput
	f.Now come out of data folder using cd ..

2.Now execute the Pairs.jar using
	hadoop jar Pairs.jar pairs.CoOccurrenceDriver
3.Now we have all the coocurrence wordpair along with the relative frequency in the part-r-00000 & part-r-00001 file in /pairsOutput folder
	to check the output: hdfs dfs -cat /pairsOutput/part-r-00000


Part2.b Stripes

For this question refer code in Project2->code->Stripes.zip file

1.Copy the cleanFile.txt from the Project2->jar->data and put in stripesInput folder using below cmd
	
	a.Please make your current directory as Project2->jar->data
	b.hdfs dfs -rmr /stripesInput/* (to remove all the existing files in input folder)
	c.hdfs dfs -mkdir /stripesInput 	(if input folder doesn't exist)
	d.move the cleanFile.txt from Project2->jar->data to /stripesInput using below cmd
	e.hdfs dfs -copyFromLocal cleanFile.txt /stripesInput
	f.Now come out of data folder using cd ..

2.Now execute the Stripes.jar using
	hadoop jar Stripes.jar stripes.StripesDriver
3.Now we have all the coocurrence freq along with the relative frequency in the part-r-00000 file in /stripesOutput folder
	hdfs dfs -cat /stripesOutput/part-r-00000



Part 3 and 4

How to run KMeans and Shortest path:

Open the file Project2->code->KMeans_Shortest.zip in eclipse to see the code.

Run Instructions:

1.Create following Input folders in hdfs with the below command: 
	a.hdfs dfs -mkdir /input
	b.hdfs dfs -mkdir /KMeansInput
	c.hdfs dfs -mkdir /SSPInput

2.There should not be any file in /input folder. So run the below command:
	hdfs dfs -rmr /input/*
	hdfs dfs -rmr /KMeansInput/*
	hdfs dfs -rmr /SSPInput/*

3.Now copy the data files from local to hdfs system. Data files has been attached along with the code in the folder Project2->jar->data. 		Current directory should be Project2->jar->data and run  the below commands:
	a.hdfs dfs -copyFromLocal centroid.txt /input
	b.hdfs dfs -copyFromLocal input-graph-small /KMeansInput
	c.hdfs dfs -copyFromLocal usrFollowersCount /SSPInput

4.You are ready to run the project. Run the KMeans_Shortest.jar file which is under Project2->jar folder.
	Execute cd .. to go in Project2->jar folder
	hadoop jar KMeans_Shortest.jar com.cse.buffalo.twittertrend.Main
5.To check the Output for KMeans open the latest file of the below format:
	/KMeansOutput+systemtime
6.To check the Output for Shortest Path open the latest file of the below format:
	/SSPOutput+systemtime

