# Timetable-Generation-Genetic-Algorithm
 Generatation of an exam timetable with certain constraints using Genetic Algorithm while employing binary encoding

## Data
We used the provided CSV files as our datasets. We read them using the CSV library and proceeded to store these datasets in a list. We made a list of student names, Teachers, Student Courses, and courses.We then removed duplicate courses from our Course List and then made a dictionary that included every student along with a list of their Courses. We also made a Dictionary of Courses that included a list of students enrolled in that course for future use.

## How the Algorithm Works (Step by Step Process) 
1. Population is generated of the length of the Total Population(No of chromosomes)
2. Fitness of each chromosome is calculated which counts the number of all constraints that are being
satisfied. The fitness is calculated by incrementing 1 to the overall score.
3. A while loop runs until the best chromosome (with the fitness of 5) is not found
4. An inner loop runs till the required number of children for that specific iteration are generated
5. Then two chromosomes are selected using roulette wheel selection which will run crossover to
generate two children
6. Then those children are mutated using the mutation function and are added to the new population.
7. After that the fitness of the new population is calculated and the old population is replaced with the
new population if the fitness of the new population is greater than the minimum of the old
population

## Core Functions Explained
- **Generate a Chromosome**:
The Constraints that we followed before assigning these were very caveman-like. We made sure that all of our courses got assigned everything. If a course had more than 30 students we divided it into 2 sections with divided up students and considered both to be separate exams. We only assigned Monday to Friday and only used 2-time slots being 9-12 and 2-5. We selected these two slots because we could only assign exams on weekdays and had 3-hour exams so these were the best slots we could think of.
- **Generate Initial Population**: 
We made 10 possible solutions and called this the initial population. Every solution was basically a dictionary that includes the exam name, date, time, week, Invigilator name room number, and a list of students as well
- **Calculate Fitness**:
To calculate fitness we simply iterated through our exam dictionary to check for clashes these clashes included the constraints that were specified in our project document. We checked by using simple 2d loops to iterate through our dictionary. For every satisfied constraint, we increased our count by 1, and this count was returned and called the fitness. The higher number it is the more efficient our solution is.
- **Roulette Wheel Selection**:
Selects two best chromosomes from population array one with the best fittest one and with the second best fitness. They are selected using probability in which the (specific chromosome fitness)/ (total fitness)
- **Crossover**:
This will generate two new children between the two chromosomes that were sent to this. (the chromosomes are taken using roulette wheel selection). We generated a random value between 0 to the length of the chromosome. We divide these chromosomes into two using the random value. (For example, a random value of 27 will create 2 separate parts one with a size of 27 and the other with the size of len(chromosome) - 27. We then take the top half of the first chromosome, and the bottom half
of the second chromosome. We then merge these and after that, we will take the bottom part of the
first and top part of the second. Finally, we returned these 2 chromosomes.
- **Mutation**:
After a lot of test runs we realized that the most common issue we had was lots of students were ending up with 2 exams on the same slot so we decided to send this method random chromosomes and we picked random exams in this and randomized the slot inside the chromosomes and selected the day and replaced it with a random new day. We noticed that our chromosomes had a lot of days without any exams so this seemed the most optimal path.

## Hard & Soft Constraints
### Hard Constraints
1. An exam will be scheduled for each course.
2. A student is enrolled in at least 3 courses. A student cannot give more than 1 exam at a time.
3. Exam will not be held on weekends.
4. Each exam must be held between 9 am and 5 pm
5. Each exam must be invigilated by a teacher. A teacher cannot invigilate two exams at the same time.
6. A teacher cannot invigilate two exams in a row.

### Soft Constraints
1. All students and teachers shall be given a break on Friday from 1-2.
2. Two hours of break in the week such that at least half the faculty is free in one slot and the rest of the faculty is free in the other slot so the faculty meetings shall be held in parts as they are now