## ASSEMBLY.PY

The `assembly.py` file serves as the master file for the application, housing wrapper functions for various features. The core logic for each feature resides in separate files, including `TaggerClassifier`, `PatternDetection_refactored`, `MySQL`, and `TagClassifier`. 

Additionally, users have the flexibility to provide arguments such as Minimum Log Time, Minimum Value of Alpha, Minimum Pattern Length, Minimum Pattern Repetition, and Maximum Pattern Length while executing the file.
<br><br>
#### `GetIntervalLogs` Function:

The `GetIntervalLogs` function begins by establishing a hashmap indexed by assignment ID and user ID, utilizing a provided list of tags. It proceeds to compute interval logs for each value using the methodology outlined in the `TaggerClassifier` file. The resulting table is then saved into a file named `Interval_logs.csv`.
<br><br>
#### `getUserHistory` Function:

Within the `getUserHistory` function, credibility scores are computed for a given list of tags. The calculation leverages the algorithms from the `TaggerClassifier` file. Following score computation, the function cleanses HTML tags from the output and records the credibility scores into a file named `userdata.csv`.
<br><br>
#### `getKrippendorfAlpha` Function:

This function is tasked with obtaining the Krippendorf Alpha value for each user. Initially, it aggregates all tag prompt IDs for the answers of a team. Subsequently, for each tag prompt ID, it collects the raters' data. This data is then passed to the `KrippendorfAlpha` function within the `TaggerClassifier`. The resulting output is written to a CSV file.
<br><br>
#### `getPatternResults` Function:

Utilizing a provided list of tags, `getPatternResults` function populates a user-assignment hashmap. Subsequently, it delegates this data to the `patternDetectionResult` function within the `PatternDetection` file. The outcomes are written to a file named `Patternrecognition.txt`.
<br><br>
#### `CalculateCredibility` Function:

This function calculates credibility scores by averaging normalized log time, alpha, and total characters.
<br><br>
#### `CombineCSVResults` Function:

The `CombineCSVResults` function consolidates all CSV and TXT files into a single file based on assignment ID and UserID. It addresses edge cases, such as those with no patterns, and computes credibility scores using the `CalculateCredibility` function.
<br><br><br>
## MySQL.py

This file facilitates connection to a MySQL database, where a dump file is currently utilized to operate the database. Once connected, the file provides helper functions for interacting with the database.
<br><br>
#### `getAnswerTags` Function:

This function executes an inner join operation on `AnswerTags` and `TagPromptDeployments`, returning a list of `AnswerTags` with associated `AssignmentID`.
<br><br>
#### `getUserTeams` Function:

`getUserTeams` retrieves all tags for a specific team across all assignments from the database. It organizes the data into a dictionary format: `{assignment_id: {team_id: {user_id: {answer_id: {tag_prompt_id: tag}}}}}`.
<br><br><br>
## TaggerClassifier.py

This component categorizes tags as either reliable or unreliable, employing various algorithms and metrics.
<br><br>
#### `BuildIntervalLogs` Function:

`BuildIntervalLogs` computes the logarithm base 2 of time differences between two consecutive tags and returns the average of the result.
<br><br>
#### `intervalLogsforTags` Function:

Within this function, interval log values are computed from a list of tags.
<br><br>
#### `compute_Krippendorff_Alpha` Function:

Utilizing the Krippendorf alpha library, this function calculates the alpha value based on a 2-dimensional array of raters and tag prompts. The calculation is omitted if there is insufficient variation.
<br><br>
#### `CalculateTagCredibilityScore` Function:

By integrating fast-tagging values and Krippendorff Alpha, credibility scores are generated for each tag ID. The score is determined by averaging normalized alpha and interval logs.
<br><br><br>

## TagClassifier.py

This file contains a function to calculate agreement/disagreement amongst peers.

We provide the function `calculateAgreementDisagreement` with a 2D array of raters and `tagpromptID`.

For each iteration of the 2D array, we get a new `tagpromptID`, and we determine the most common rating for that ID. It then calculates the fraction of users who agree with the common rating and who don’t. The values are returned by the function in the form of a dictionary.
<br><br><br>
## CSV Files
<br>

1. **Interval_logs.csv:**
   - Column Names: Assignment_id, User_id, IL_result, Time, Number_of_Tags
<br>

2. **Krippendorff.csv:**
   - Column Names: Assignment_id, Team_id, User_id, Alphas
<br>

3. **User_data.csv:**
   - Column Names: User_id, Assignment_id, Question, Score, Review_Comment, Tag_Prompt, Tag_Value, Credibility_Score
<br>

4. **Answers.csv:**
   - Column Names: id, question_id, answer, comments, response_id
