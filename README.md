# Election_Analsysis

## Project Overview 
A Colorado Board of Election employee has given you the following tasks to complete the election audit of a recent local congressional election. 

1. Calculate the total number of votes cast. 
2. Get a complete list of candidates who received votes. 
3. Calculate the total number of votes each candidate receive. 
4. Calculate the percentage of votes each candidate won. 
5. Determine the winner of the election based on populer vote. 

## Resources 
- Data Source: election_results.csv 
- Software: Python 3.7.6, Visual Studio Code, 1.38.1 

## Election Audit Results 
The analysis of the election show that: 
- There were 369,711 votes cast in the election. 
- The counties that particiated in the election were: 
  - Jefferson county with 38,855 votes and 10.5% of the total votes.
  - Denver county with 306,055 votes and 82.8% of the total votes. 
  - Arapahoe county with 24,801 votes and 6.7% of the total votes.

The county with the largest number of votes: 
  - Denver

- The candidates were: 
  - Charles Casper Stockham
  - Diana DeGette
  - Raymon Anthony Doane
- The candidate results were: 
  - Charles Casper Stockham received 23.0% of the vote and 85,213 votes. 
  - Diana DeGette received 73.8% of the vote and 272,892 votes. 
  - Raymon Anthony Doane received 3.1% of the vote and 11,606 votes. 

The winner of the election by popular vote: 
Diana DeGette 

![Screen Shot 2021-11-11 at 1 18 26 PM](https://user-images.githubusercontent.com/92831268/141371894-da5839fb-22e4-4cf5-98ac-fc7eaf6ef2ff.png)

## Election Audit Summary 
The code withing the attached PyPoll_Challenge.py was the code developed to conduct the election results audit. This script could realistically be used for any election to audit the results. If we wanted to create a audit for a different set of counties, the only piece of code that would change is the csv document uploaded in line 3 of the code. This code also would work on a set of data that had many candidates and over more counties, this data set just happens to only have three. Since there are two for loops that loop through the data and conduct new counts for every candidate or county, if there is an additional county added to the list, the fomula would count it as a new county (or new counties) and would produce a similar looking output. If you wanted to use this for presidential elections, you could alter the script to instead of list counties, list states. (county_names becomes state_names, and county_votes becomes state_votes), and adjust all subsequent script to match state instead of county data. In this case, you would also have to ensure that the headers in the CSV file matched the headers we are indicating in the script. In this case, the candidate header is in column 3 (row[2]) and the county is in column 2 (row[1]). If the header were to change in apresidential election and have Ballot ID, Candidate, State the header we are looking for would switch and we would have to change it in the 'for row in header' loop. 

This is the location where if you need to upload a different CSV file, this is where you would reference it. Instead of "election_results", the new csv file and another data would be referenced here. 

<img width="522" alt="Screen Shot 2021-11-11 at 2 12 58 PM" src="https://user-images.githubusercontent.com/92831268/141376406-55e27063-c2ce-46b2-9eff-1c7750854db3.png">

This is where you would change county to state. 

<img width="436" alt="Screen Shot 2021-11-11 at 2 10 51 PM" src="https://user-images.githubusercontent.com/92831268/141376249-c0e7fe97-a562-4721-8c87-cc0d1542d881.png">

This is where you need to ensure that the appropriate header is being selected for the information desired.

<img width="385" alt="Screen Shot 2021-11-11 at 2 11 03 PM" src="https://user-images.githubusercontent.com/92831268/141376295-f8783c84-ac16-4496-9b6b-c0c68a91f735.png">
