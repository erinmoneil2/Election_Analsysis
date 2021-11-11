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
The following code was the code developed to conduct the election results audit. This script could realistically be used for any election to audit the results. If we wanted to create a audit for a different set of counties, the only piece of code that would change is the csv document uploaded in line 3 of the code. This code also would work on a set of data that had many candidates and over more counties, this data set just happens to only have three. Since there are two for loops that loop through the data and conduct new counts for every candidate or county, if there is an additional county added to the list, the fomula would count it as a new county (or new counties) and would produce a similar looking output. If you wanted to use this for presidential elections, you could alter the script to instead of list counties, list states. (county_names becomes state_names, and county_votes becomes state_votes), and adjust all subsequent script to match state instead of county data. In this case, you would also have to ensure that the headers in the CSV file matched the headers we are indicating in the script. In this case, the candidate header is in column 3 (row[2]) and the county is in column 2 (row[1]). If the header were to change in apresidential election and have Ballot ID, Candidate, State the header we are looking for would switch and we would have to change it in the 'for row in header' loop. 


import csv
import os

file_to_load = os.path.join("Resources", "election_results.csv")

file_to_save = os.path.join("analysis", "election_results.txt")

total_votes = 0

candidate_options = []
candidate_votes = {}

county_names = []
county_votes = {}

winning_candidate = ""
winning_count = 0
winning_percentage = 0

largest_county_turnout = ""
largest_county_count = 0

with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)

    # For each row in the CSV file.
    for row in reader:
        # Add to the total vote count
        total_votes = total_votes + 1
        # Get the candidate name from each row.
        candidate_name = row[2]
        # 3: Extract the county name from each row.
        county_name = row[1]

        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:
            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)
            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0
        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        # 4a: Write an if statement that checks that the
        # county does not match any existing county in the county list.
        if county_name not in county_names:
            # 4b: Add the existing county to the list of counties.
            county_names.append(county_name)
            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0
        # 5: Add a vote to that county's vote count.
        county_votes[county_name] += 1

with open(file_to_save, "w") as txt_file:

    # Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)

    # 6a: Write a for loop to get the county from the county dictionary.
    for county in county_votes:
        # 6b: Retrieve the county vote count.
        county_vote = county_votes[county]
        # 6c: Calculate the percentage of votes for the county.
        county_percentage = int(county_vote)/int(total_votes) * 100
        county_results = (
            f"{county}: {county_percentage:.1f}% ({county_vote:,})\n")
         # 6d: Print the county results to the terminal.
        print(county_results, end="")
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)

         # 6f: Write an if statement to determine the winning county and get its vote count.
        if (county_vote > largest_county_count):
            largest_county_count = county_vote
            largest_county_turnout = county
          
    # 7: Print the county with the largest turnout to the terminal.
    largest_county_turnout = (
        f"------------------------\n"
        f"Largest County Turnout: {largest_county_turnout}\n"
        f"------------------------\n"
    )
    print(largest_county_turnout)
    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(largest_county_turnout)
    # Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
        # Print each candidate's voter count and percentage to the
        # terminal.
        print(candidate_results)
        #  Save the candidate results to our text file.
        txt_file.write(candidate_results)

        # Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

    # Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

    # Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
