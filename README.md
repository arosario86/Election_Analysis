# Election_Analysis
Seth has asked me to calculate election data to see who the winning candidate is, along with the total number of election votes casted.
My goal was to review the total number of votes cast, complete list of candidates who have received votes, percentage of votes won by each candidate, the total number of votes each candidate won, as well as the winner of the election based on the popular vote.

## Resources used: election_results.csv
Python 3.7.6 and Visual Studio Code

## Summary
There were a total of 369,711 votes casted.
Candidates were Charles Casper Stockham, Diana DeGette, and Raymon Anthony Doane.
Charles Casper Stockham received 23%, Diana DeGette received 73.8%, and Raymon Anthony Doane received 3.1%.

# Challenge
Added the following to my Visual Studio Code to print to my terminal:
# -*- coding: UTF-8 -*-
"""PyPoll Homework Challenge Solution."""

Add our dependencies.
import csv
import os

Add a variable to load a file from a path.
file_to_load = os.path.join("Resources","election_results.csv")
Add a variable to save the file to a path.
file_to_save = os.path.join("Analysis", "election_results.txt")

Initialize a total vote counter.
total_votes = 0

Candidate options and candidate votes.
candidate_options = []
candidate_votes = {}

1: Create a county list and county votes dictionary.
county_list = []
county_votes = {}

Track the winning candidate, vote count and percentage
winning_candidate = ""
winning_count = 0
winning_percentage = 0

2: Track the largest county and county voter turnout.
largest_winning_county = ""
largest_winning_count = 0
largest_winning_percentage = 0

Read the csv and convert it into a list of dictionaries
with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    Read the header
    header = next(reader)

    For each row in the CSV file.
    for row in reader:

        Add to the total vote count
        total_votes = total_votes + 1

        Get the candidate name from each row.
        candidate_name = row[2]

        3: Extract the county name from each row.
        county_name = row[1]

        If the candidate does not match any existing candidate add it to
        the candidate list
        if candidate_name not in candidate_options:

            Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0

        Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1

        4a: Write a decision statement that checks that the
        county does not match any existing county in the county list.
        if county_name not in county_list:

            4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0

        5: Add a vote to that county's vote count.
        county_votes[county_name] += 1


Save the results to our text file.
with open(file_to_save, "w") as txt_file:

    Print the final vote count (to terminal)
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)

    6a: Write a repetition statement to get the county from the county dictionary.
    for county_name in county_votes:
        6b: Initialize a variable to hold the county’s votes as they are retrieved from the county votes dictionary.
        all_votes = county_votes[county_name]
        6c: Calculate the percent of total votes for the county.
        all_votes_percentage = (float(all_votes) / float(total_votes)) * 100

         6d: Print the county results to the terminal.
        county_results = (f"{county_name}: {all_votes_percentage:.1f}% ({all_votes:,})\n")
        print(county_results)

         6e: Save the county votes to a text file.
        txt_file.write(county_results)

         6f: Write a decision statement to determine the winning county and get its vote count.
        if (all_votes > largest_winning_count) and (all_votes_percentage > largest_winning_percentage):
            largest_winning_count = all_votes
            largest_winning_percentage = all_votes_percentage
            largest_winning_county = county_name
            
    7: Print the county with the largest turnout to the terminal.
    winning_county_summary = (
        f"\n-------------------------\n"
        f"Largest Winning County: {largest_winning_county}\n"
        f"-------------------------\n")
    print(winning_county_summary, end="")
    
    8: Save the county with the largest turnout to a text file.
    txt_file.write(winning_county_summary)

    Save the final candidate vote count to the text file.
    for candidate_name in candidate_votes:

        Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

        Print each candidate's voter count and percentage to the
        terminal.
        print(candidate_results)
        Save the candidate results to our text file.
        txt_file.write(candidate_results)

        Determine winning vote count, winning percentage, and candidate.
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage

    Print the winning candidate (to terminal)
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)

    Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
    
  ![2022-07-04 (1)](https://user-images.githubusercontent.com/104965708/177200113-ba133ddb-8782-4805-9e76-79d3779b2121.png)
     
### Overview of Election Audit
The overall goal was to identify the winning county and winning candidate during this election.
The winning county was Denver, with 82.8% (306,055 total votes).
The winning candidate was Diana DeGette with 73.8% (272,892 votes).

### Election Audit Results
* Total Votes: 369,711
* County Votes
  * Jefferson: 10.5% (38,855)
  * Denver: 82.8% (306,055)
  * Arapahoe: 6.7% (24,801)
* Denver had the largest number of votes
* Candidate Votes 
  * Charles Casper Stockham: 23.0% (85,213)
  * Dianna DeGette: 73.8% (272,892)
  * Raymon Anthony Doane: 3.1% (11,606)
* Diana DeGette won the election with a total of 272,892 votes, a percentage of 73.8% of the votes.
* 
## Summary
This script can be used for future elections by running the total votes and comparing each candidate to see who won each election. This can be used for different counties by adding the new counties to the list using append function to edit the current lists. This will enable the state to see winning counties and their winning candidates by the push of a button (run button). Both the candidates list and counties list will need to be modified when using this script for different counties within the state. This initial analysis only looked at 3 counties and 3 candidates.
