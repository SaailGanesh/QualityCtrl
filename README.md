# Quality Control of Crowd Labeling
This repository is created for Quality Control of Crowd Labeling Project under Professor Edward Gehringer. 

<br>

## Abstract
Peer-assessment-based educational methods are becoming more widespread. These methods involve students reviewing projects and comments created by their peers and providing suggestions for improvement. However, the effectiveness of this process depends on the quality of the comments in the reviews. We have devised natural-language processing approaches to evaluate review comments based on machine learning. The accuracy of these approaches depends on the quality of the training data.  Our training data consists of comments labeled by students as containing or not containing certain characteristics, such as suggestions or explanations.  This paper reports on our strategies for automatically vetting labels (“tags”) assigned by students.

But can we validate the quality of student tagging?  To measure the quality of individual tags, as well as the reliability of the student taggers, several strategies have been implemented. The first strategy attempts to identify students who tag “too fast,” and assign tags so quickly that they could not have given them adequate consideration.  Another approach is to exclude tags where different students disagree on whether the comment should or should not have been tagged.  A third metric looks for “anti-patterns,” such as all tags set to yes, all tags set to no, alternating yes and no, or repeated sequences such as “yes, yes, no, yes, yes, no, yes, yes, no.”  The final approach is “labeler calibration,” where tags assigned by a student are compared with tags that would be predicted from the training data that we have previously collected. This research aims to assign reliability metrics to each tag and tagger, and provide these metrics to researchers, who will be able to derive machine-learning training datasets by filtering the tags to create datasets with only the most reliably tagged data, or larger datasets that also include less-reliable tags.

<br>

## Database Tables used:

**ALL THE HYPERLINKS ARE NOT WORKING**

Link to all the Tables in the Database: [Documentation on Database Tables](https://expertiza.csc.ncsu.edu/index.php/Documentation_on_Database_Tables)

<div align="center">
  <br>
   <img src="https://i.imgur.com/BRIY6cj.png" alt="" width="700" height="700">
  <br><br><br>
</div>

**Tables Used:**

<div align="center">
  <br>
  <a href="https://expertiza.csc.ncsu.edu/index.php?title=Answer_tags"><img src="https://i.imgur.com/dAPeTKZ.png" alt="" width="600" height="300"></a>
  <br><br><br>
  
  <a href="https://expertiza.csc.ncsu.edu/index.php?title=Answers"><img src="https://i.imgur.com/aM3iRG8.png" alt="" width="600" height="300"></a>
  <br><br><br>
  
  <a href="https://expertiza.csc.ncsu.edu/index.php?title=Tag_prompt_deployments"><img src="https://i.imgur.com/xrVrgsU.png" alt="" width="1100" height="300"></a>
  <br><br><br>
  
  <a href="https://expertiza.csc.ncsu.edu/index.php?title=Teams_users"><img src="https://i.imgur.com/vjBEOMp.png" alt="" width="600" height="200"></a>
  <br><br><br>
  
  <a href="https://expertiza.csc.ncsu.edu/index.php?title=Submission_records"><img src="https://i.imgur.com/sWLuIi3.png" alt="" width="600" height="300"></a>
  <br><br><br>
</div>


## Quality Control - Setup and Execution

<br>

### For Windows

#### Installing Chocolatey and MySQL on Your System

**Installing Chocolatey for MySQL on Windows**

To set up Chocolatey and MySQL on your system, follow these steps:

<br>

1. **Install Chocolatey Software:**
   Go to the [Chocolatey website](https://chocolatey.org/) and follow the instructions provided in the article. Execute the commands in PowerShell as mentioned on the website.

<br>

2. **Install MySQL:**
   After Chocolatey installation, open an administrative PowerShell and enter the following command:

   ```powershell
   choco install mysql
   ```

   Ignore any red output, and when prompted, grant multiple permissions by typing "Y."

<br>

3. **Install MySQL-Python:**
   Next, enter the following command:

   ```powershell
   choco install mysql-python
   ```

   If there are no errors, the installation is successful. You can find the MySQL command prompt in the start menu to start working.

   Note: You might need to restart your computer.

<br>

4. **MySQL Password:**
   The default username is "root," and the password is blank.

<br>

### Creating the Expertiza Database Locally

1. **Obtain the Database Dump File:**
   Request access to the database dump file from your professor. Download and save it in your working directory; the filename might be "expertiza_production.sql" or "expertiza_production_backup.sql."

<br>

2. **Create the Database:**
   Open your command prompt and enter the following commands:

   ```bash
   mysql -u root -p
   ```

   Press Enter when prompted for the password (leave it blank), then execute the following commands:

   ```sql
   CREATE DATABASE IF NOT EXISTS expertiza_production;
   USE expertiza_production;
   ```

   Exit the database by typing "exit."

<br>

3. **Populate the Database:**
   In the command prompt, navigate to the directory containing "expertiza_production_backup.sql" and run the following command:

   ```bash
   mysql -u root -p expertiza_production < expertiza_production_backup.sql
   ```

   Press Enter when prompted for the password (leave it blank). The process may take some time.

<br>

### Executing the Developed Code

1. **Download or Clone the Project:**
   Obtain the project from the [GitHub repository](https://github.com/repository-link). Use the following command to clone the repository:

   ```bash
   git clone [repository-link]
   ```

<br>

2. **Install Dependencies:**
   Navigate to the cloned directory and run the following command in the command prompt or your IDE's terminal:

   ```bash
   pip install -r requirements.txt
   ```

   This will install all required dependencies.

<br>

3. **Run the Main File:**
   The main file, "Assembly.py," handles processes from connecting to the database to generating output files. Run the file in an IDE like VS Code or use the command:

   ```bash
   python Assembly.py
   ```

   The output will be stored in a new directory named "data."
