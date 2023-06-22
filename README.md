# Relevant Coursework

Code for the following assignments are available upon request. For access to the private repos with my work, feel free to email me at [ckboyd@uchicago.edu](mailto:ckboyd@uchicago.edu).

## CAPP 121: Computer Science with Applications 1

Programming Assignments:
* [Modeling Epidemics](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa1/index.html) (Introduction to Programming)
  * *Summary:* This first assignment provided an introduction to basic programming concepts and skills. In this assignment, I wrote a script to simulate a simplified version of the SIR epidemic model. My code modeled how infection spreads through a city from residents to their neighbors.
  * *Topics covered:* control flow statements (for loops, while loops), data types (lists, tuples, strings, integers, floats, booleans)
* [Modeling Language Shifts](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa2/index.html) (Functions)
  * *Summary*: This assignment provided an introduction to defining and using functions. In this assignment, I implemented a variation of the language shift model described by Beltran, et al. in their paper [A Language Shift Simulation Based on Cellular Automata](https://www.researchgate.net/publication/259557981_A_Language_Shift_Simulation_Based_on_Cellular_Automata) to model how use of language shifts depending on neighborhood characteristics.
  * *Topics covered:* anatomy of a function, default parameters, return statements, manual and automatic testing
* [Analyzing Candidate Tweets](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa3/index.html) (Dictionaires and File Basics)
  * *Summary:* This assignment provided an introduction to python dictionaries and working with multiple files. For this assignment, I analyzing tweets sent from the official Twitter accounts of four British political parties: the Conservative and Unionist Party (@Conservatives), the Labour Party (@UKLabour), the Liberal Democrats (@LibDems) and the Scottish National Party (@theSNP) during purdah. I looked at favorite hashtags, most frequent mentions, and most frequent phrases used by different political parties.
  * *Topics covered:* dictionaries, sets, nested dictionariess, comprehensions, decomposition, abstraction, k-mers
* [Polling Places](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa4/index.html) (Classes and Objects)
  * *Summary:* The goal of this assignment is to practice designing and implementing classes and methods, and working with class instances. In this assignment, I wrote code to simulate the flow of voters through polling places and analyze the interplay the number of voting booths assigned to a precinct and the amount of time voters spend waiting in line.
  * *Topics covered:* stacks, queues, object-oriented programming, classes, attributes (class vs. instance attributes), methods (e.g. dunder)
* [Linear Regression](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa5/index.html) (NumPy)
  * *Summary:* For this assignment, I fit linear regression models and implement a few simple feature variable selection algorithms. The assignment gave me experience with NumPy and more practice with using classes and functions to support code reuse.
  * *Topics covered:* NumPy, operations on arrays (creating, shaping, slicing, indexing, fancy indexing)
* [Visualizing Avian Biodiversity Using Treemaps](https://classes.cs.uchicago.edu/archive/2022/fall/30121-1/pa/pa6/index.html) (Recursion)
  * *Summary:* This assignment provided an opportunity to create higher-order functions, recursive functions, and recursively-defined data structures. I wrote code to generate treemaps to visualize this avian biodiversity data from samples taken throughout the year.
  * *Topics covered:* trees, recursion, binary search tree, data visualization


## CAPP 122: Computer Science with Applications 2

Programming Assignments:
* [Markovian Candidate](https://github.com/claireboyd/capp_coursework/tree/main/capp_122/markovian_candidate) (Program Structure)
  * *Summary:* For this assignment, I explored the basics of software organization & structure in a Python program. I developed a modeling system using Markov Models, which can be used to capture the statistical relationships present in a language like English. One application of Markov models is in analyzing actual text and assessing the likelihood that a particular person uttered it. For this assignment, we used speeches from presential candidates to figure out which candidate was more likely to deliver each speech. I implemented this using custom hash tables by writing my own hash function.
  * *Topics covered:* hash tables, virtual environments, creating modules, abstract classes, interfaces
* [Scraping Chicago Parks](https://github.com/claireboyd/capp_coursework/tree/main/capp_122/scraping_chicago_parks) (Web Scraping)
  * *Summary:* I built a scraper that crawls a simulacrum of the Chicago Parks website to construct a search index. The assignment gave me experience building a real-world crawler that works with HTML documents as well as additional practice composing a Python application.
  * *Topics covered:* data formats (binary, text-based), HTTP requests, web scraping, APIs, HTML parsing, CSS selectors
* [Chicago Parks Search Engine](https://github.com/claireboyd/capp_coursework/tree/main/capp_122/chicago_parks_search_engine) (Querying in SQLite)
  * *Summary:* I built a simple search engine to query a database of chicago public parks. The assignment gave me experience using regular expressions, building simple to complex queries uqing SQLite, and better understanding of the connection between backend data work and user interface and design.
  * *Topics covered:* SQL queries, regular expressions, user interface and design
* [Fuzzy Matching Paycheck Protection Program (PPP) with Illinois Campaign Finance Data](https://github.com/claireboyd/capp_coursework/tree/main/capp_122/record_linkage) (Data Linkage)
  * *Summary:* I implemented [Jaro-Winkler](https://en.wikipedia.org/wiki/Jaro%E2%80%93Winkler_distance) similarity to fuzzy match organizations in two different datasets. The assignment gave me the opportunity to faciliate a data cleaning process, use simple to complex regular expressions, and think through different ways to a single (and expensive) data task for computational efficiency.
  * *Topics covered:* data linkage, fuzzy matching, regular expressions, computational efficiency
* [Predicting Diabetes with Decision Trees](https://github.com/claireboyd/capp_coursework/blob/main/capp_122/decision_trees/README.Md) (Introduction to Machine Learning Models)
  * *Summary:* For this assignment, I learned how to build a recursive, decision tree model for a binary classificaiton task (does a person with given characteristics have diabetes or not?). This last assignment taught me the importance of non-linear activation functions, how to incorporate tie breakers, and (more generally) start building an intuition behind what machine learning models can help do successfully.
  * *Topics covered:* decision trees, recursion, train/test split, activation functions, information gain, gini coefficient
