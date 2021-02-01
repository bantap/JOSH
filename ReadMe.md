# JOb Search Helper (JOSH)
### An 18-Week Web Application Project in ASP.NET MVC Core for MSSA

---

Paul Banta <br />
MSSA CAD <br />
January, 2021

---

### JOb Search Helper (JOSH)

#### ➪ Introduction

The JOb Search Helper website was originally conceived as a Job Search Records web application.
After a little thought, a slight rename seemed to be in order.
While the name "Job Search Records" accurately captures what the website will do, it doesn't fully convey the reason why someone would (want to) use this application - to **help** them find a job.
Therefore, the name has been changed to JOb Search Helper, which brings out the idea of Helping a little better.
In addition, it also lends itself to an acronym: JOSH.

The JOSH web application (website) will help users who are actively applying for jobs.
First, it will help them to **organize** their job search. Most job applications ask for very similar information.
JOSH will allow users to organize that information.
The hope is that by being organized, users will be more efficient and will be able to apply to a greater number of jobs (more job applications each day, each week, each month).
Second, JOSH will help users to be more **thorough** with job applications that start to materialize.
When an employer (job application) shows interest in the candidate, JOSH will organize and keep track of the interactions between the candidate and the employer.
This will include keeping track of future interactions such as upcoming interviews, form submissions, etc..

---

#### ➪ Organize

**Application Helper**

When filling out job applications, most employers ask candidates to provide very similar pieces of information.
Different employers tend to ask for similar information.
A job application will typically ask the candidate to provide the following:
+ Name, Address, Phone Number, Birthdate, ect.
+ Previous Job History
  + Company, Dates, Location, Brief Description
+ Education History
+ References
+ Resume

The JOSH system will allow users to enter in and store their Previous Job History, their Education History, and their References.
This will provide users with the capability of copying and pasting these pieces of information (which are common on most job applications) from JOSH into each and every different job applications that the user fills out.
The copy-and-paste will not be automated.
It will still be a manual process.
However, JOSH will store all of the user's common information in a single place.

Previous Job History, Education History, and References are each Lists of specific kinds of information.
JOSH will provide one additional List of information that the user can maintain: Company Research. Websites such as GlassDoor, Indeed, and possibly even StackOverflow allow their users to rate their own companies (the company that they work for).
This information is freely available on the web and typically includes an overall rating as well as salary ranges.
JOSH will allow users to store Company Research information in a separate list.
This list of Company Research, while not useful in filling out job applications, would be helpful for narrowing in and focusing on the best companies to work for.
Job seekers could use this list to help decide which companies they should spend more time applying at and which companies they should spend less time applying at.

**What JOSH Is Not**

JOSH will not store the user's Name, Address, Phone Number, etc.. Users will know all of this information from memory.

JOSH will not store the user's Resume.
A Resume, with all of it's elegant formatting (layout, fonts, etc.), is best written using a word processor such as Microsoft Word or Google Docs.

---

#### ➪ Thorough (follow-through, persistent, nothing falls through the cracks)

**List Of Job Applications**

As a user fills out job applications online, he/she will have the ability to enter each job application into JOSH.
JOSH will have fields for Date Posted, Date Applied, Company, Job Number Reference, Job Title, Job Location, Job Description, and Salary Range (and possibly others).
JOSH will also provide a check-box to allow the user to hide jobs that he/she didn't get (in order to keep the list shorter by only showing "Active" jobs).

**List Of Correspondence**

For each job in the list of Job Applications, JOSH will allow the user to maintain the details of all of the correspondence that he/she has had with that employer. This may include emails, phone conversations, and in-person meetings such as interviews. This list will allow for interactions that are scheduled in the future such as interview dates / times. Future interactions with all employers will be listed on the main user page when the user logs in. As an example, the correspondence for a specific job application might be something like:
1. Jan 1st | Submitted Job Application | Online
1. Jan 13th | Received an email asking about my availability to interview | Email
1. Jan 13th | Replied to email | Email
1. Jan 14th | Received a phone call from Bob Smith confirming the interview date and time | Phone call
1. Jan 21st | Interview | In-Person

---

[Database Diagram](JOSHDatabaseDiagram.pdf)
