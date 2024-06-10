# TUSA

TUSA(Transylvania University Scheduling Assistant) is an automatic scheduling website that attempts to remedy the stressful situation of students scheduling for their four years at college. I developed this project alongside three other people for my senior project. TUSA guarantees a valid four year plan for students while also taking into account their interests when devising the schedule. Students can input their preferences of what classes and programs they want and do not want to take, what major they want to schedule for, and how many years they want to schedule for. TUSA also has several other features such as graduation progress, notes they can keep with other students and professors, the course catalog, and a personalized calendar. 

## Using TUSA 

Link to TUSA: http://www.cs.transy.edu/TUSA/js-login/front/build/

Username: Username

Password: Password*1

The Automatic Schedule tab can be found under Plan & Schedule on the navigation bar. If you prefer to make a new account on the login page, the email portion requires a Transylvania University formatted email, which is username@transy.edu. Also to use the automatic scheduler, you must first declare a major. The provided account has already declared themselves as a Computer Science major, but this can be changed under Major Declaration also under Plan & Schedule.

<img width="739" alt="Screenshot 2024-04-23 at 3 12 58 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/547a69cf-46b4-43ae-923e-d7190b1fb3d6">

### TUSA Homepage

<img width="1280" alt="Screenshot 2024-04-23 at 12 56 21 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/1d5b57c4-66a1-4d3b-980f-53f752840952">

<img width="1277" alt="Screenshot 2024-04-23 at 12 56 39 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/6f714397-ace6-4283-a9b5-0b3b8db48a7a">

## Declaring Information in TUSA

<img width="1273" alt="Screenshot 2024-04-23 at 2 03 52 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/cc9e276a-4599-44e6-a47d-353e1a83024d">

<img width="1273" alt="Screenshot 2024-04-23 at 2 03 34 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/dfe3ab0b-ab3d-470a-b9e6-b36b7552b64b">

## Generated Schedule in TUSA

<img width="1127" alt="Screenshot 2024-04-23 at 1 00 33 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/7a1c91f3-3f06-4ccd-963d-3520f9d6f31a">

<img width="1195" alt="Screenshot 2024-04-23 at 2 02 51 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/36769076-4986-4264-b44e-9a751a42f459">

<img width="1195" alt="Screenshot 2024-04-23 at 2 03 03 PM" src="https://github.com/KeatonGoebel/TUSA/assets/155006422/f187a2aa-a960-4718-ae5b-3132b4d5ae12">

#### Developing TUSA

Our group was given three months to plan and design our project and an additional three months to implement it. We decided it would be best to split the group into two pairs, with two people working primarily on the front-end and two people working primarily on the back-end. I worked on the back-end, which involved setting up the products database in MySql, the automatic scheduling algorithm in Python, and a Shell Script. Starting with the database, we were careful to use third normal form. This meant that things like each category of user preferences was given its own table. Everytime the user interacts with the website, such as creating an account, declaring a major, or setting their preferences, this information is saved in the database. During login, we also implemented a password hashing system to increase security. Therefore, user passwords are never saved in the database in a readable format. 

The automatic scheduler is a constraint-based forward and backtracking algorithm. It uses forward checking to detect courses that will cause problems and remove them from the course list, dramatically reducing the number of recursive iterations. Additional constraints were added throughout the process which dramatically improved performance. If the user already took a certain course, or if the course is not offered a certain year, or if the user does not meet the prerequisites, then it would be removed from the course list. Every iteration of the algorithm creates a constrained course list and then it generates a list of potential schedule solutions based on that list. For this list of schedule solutions, each is given a score based on how closely it aligns with user preferences. If the user requests a certain course and that course is in the schedule, then the schedule will have a higher score. The semester schedule with the highest score that is also a valid schedule will be selected to be added to the full schedule. Whether a semester is valid or not depends on the major and the current semester. For the current semester, a certain amount of general education requirements and electives are required for each semester to guarantee the user meets them all. For the major, the user has to take certain classes at certain times to guarantee they have all the prerequisites and can complete the major.  

Three plain-text files were leveraged to integrate the database, website, and algorithm. Whenever the algorithm is called from main, it starts by querying the database and writing information from the database to a file called usernameProfile1.txt. This file holds all relevant information the algorithm will need like the user’s degree, their class status, and all of their preferences. Throughout the duration of the algorithm however, it uses a second text file called usernameNewProfile.txt. This second text file is rewritten at the end of every semester. If the current semester was Fall, the next version of usernameNewProfile will have the current semester as Winter. The class status, current semester, current year, and list of classes taken all change in this file throughout the duration of the algorithm. The third text file is simply called username.txt. At the end of every semester, the chosen semester schedule is written to the username. Therefore at the end of the algorithm, usernameProfile1 holds all the starting information, usernameNewProfile holds all the ending information, and username holds the resulting schedule. 

The Final part of TUSA's backend was a Shell script. The algorithm was implemented to only run for one semester at time. It takes in a text file, and writes a semester schedule onto username.txt. Our Shell script was helpful because it allowed us to easily call the algorithm over and over again based on the output. It could call the algorithm a different number of times based on the status of the user or stop calling the algorithm if an error message is found in one of the text files. 

##### Challenges and Conclusions 

Because of our time constraints, we decided it would be best early on to reimplement an already existing algorithm from a project that was similar to ours. While this decision meant that our code was up and running much faster, it also meant that the code base for our algorithm would be in Python. Python’s extensive features made the process of coding the algorithm much easier and more efficient. However, this choice also exacerbated our algorithm’s performance problems. As the algorithm got increasingly slow as the course list grew we decided to run the algorithm with only a sample of the school course list. Additionally, we also realized it would be impossible to implement every major the school has to offer. Every major requires us to implement the sequence of courses it requires in order to graduate. We decided on five different majors that represent a diversity of departments and also reflected some of the most popular majors in the school to help as many people as possible. Those selected majors were Computer Science, Biology, Business Administration, Digital Arts and Media, and French Language and Literature. Given the limitations we faced, we all felt that TUSA was an impressive piece of software and we were proud of what we accomplished. 

