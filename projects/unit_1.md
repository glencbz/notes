# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 

##Project Submission
1. Ensure that a soft launch of your project is up on github pages by Wednesday 5th October 2016.
2. Submit your Project 1 repository details at the Project 1 submission page before 8AM on Friday 7th October 2016. 
3.  Ensure that the master and gh-pages branches contain your latest project codes.

## Presentation format
* Presentations are 8 mins: 5 mins presentation and 3 mins feedback/Q&A
* Students to present one project (Either project 1A or 1B)
* Order of student presentations will be written on the board at the start of the day at 9AM. The presentation order will be random.
* Student before the current presenter to give feedback in the form of one glow comment (One great thing about their project)
* Student after the current presenter to give feedback in the form of one grow comment (A possible improvement to their project)

###Things to mention during your presentation: 
* Explain what your game is about and demo it
* Talk about your planning process
* Show your code
* Explain how you organized your code
* Share interesting code solutions
* Talk about any issues encountered during the project and how you overcame them.

---
#1a: Quiz Game 

## Trivia Quiz
Create A simple trivia quiz  using Javascript, HTML and CSS.

##### Game Instructions:

2 players take turns to answer a series of questions. Questions can either be true/false or multiple choice questions. The person with the most correct answers out of 10 questions wins. The questions are randomised so one can play multiple times with different questions showing up each time.

Sample Games: To be shown in class.

**You will need to declare the following functions:**

#### numberOfQuestions()
It should return an integer that is the number of questions in a game

#### currentQuestion()
It should return an integer that is the zero-based index of the current question in the quiz

#### correctAnswer()
It should return an integer that is the zero-based index the correct answer for the currrent question

#### numberOfChoices()
It should return an integer that is the number of choices for the current question

#### playTurn(choice)
It should take a single integer, which specifies which choice the current player wants to make.
It should return a boolean true/false if the answer is correct.

#### isGameOver()
It should return a true or false if the quiz is over.

#### whoWon()
It should return 0 if the game is not yet over,
else it should return either 1 or 2 depending on which player won.
It should return 3 if the game is a draw.

#### restart()
It should restart the game so it can be played again.

#### Assumptions
Players take turns to answer the questions. After one player has answered, it will automatically be the next player's turn to answer.

#1b: The Game

### Overview

Let's start out with something fun - **a game!**

Everyone will get a chance to **be creative**, and work through some really **tough programming challenges** – since you've already gotten your feet wet with Tic Tac Toe, it's up to you to come up with a fun and interesting game to build.

**You will be working individually for this project**, but we'll be guiding you along the process and helping as you go along. Show us what you've got!

### Technical Requirements

Your app must:

* **Render a 2-player game in the browser**
* **Design logic for winning** & **visually display which player won**
* **Include separate HTML / CSS / JavaScript files**
* Stick with **KISS (Keep It Simple Stupid)** and **DRY (Don't Repeat Yourself)** principles
* Use **Javascript or jQuery** for **DOM manipulation**
* **Deploy your game online**, where the rest of the world can access it
* Use **semantic markup** for HTML and CSS (adhere to best practices)

---

### Necessary Deliverables

* A **working game, built by you**, hosted somewhere on the internet
* A **link to your hosted working game** in the URL section of your Github repo
* A **git repository hosted on Github pages**, with a link to your hosted game on the shared repository, and frequent commits dating back to the very beginning of the project.
* **A ``readme.md`` file** with explanations of the technologies used, the approach taken, usage instructions, unsolved problems, etc.

---

### Project Feedback + Evaluation

* __Project Workflow__: Did you complete the user stories, wireframes, task tracking, and/or ERDs, as specified above? Did you use source control as expected for the phase of the program you’re in (detailed above)?

* __Technical Requirements__: Did you deliver a project that met all the technical requirements? Given what the class has covered so far, did you build something that was reasonably complex?

* __Creativity__: Did you add a personal spin or creative elements to your project? Did you deliver something of value to the end user (not just a login button and an index page)?

* __Code Quality__: Did you follow code style guidelines and best practices covered in class (i.e spacing, modularity and semantic naming)? Did you comment your code as your instructor has in class?

* __Deployment__: Did you deploy your application to a public url using GitHub Pages?

* __Total__: Your instructor will give you a total score for your project between:
    
| Score| Expectations |
| :----:| :---------: |
| **0** | _Incomplete._ |
| **1** | _Does not meet expectations._ |
| **2** | _Meets expectations, good job!_ |
| **3** | _Exceeds expectations, you wonderful creature, you!_ |

This will serve as a helpful overall gauge of whether you've met the project goals, but __the more important scores are the individual ones__ above, which can help you identify where to focus your efforts for the next project!

---


### Suggested Ways to Get Started

* **Break the project down into different components** (data, presentation, views, style, DOM manipulation) and brainstorm each component individually. Use whiteboards!
* **Use your Development Tools** (console.log, inspector, alert statements, etc) to debug and solve problems
* Work through the lessons in class & ask questions when you need to! Think about adding relevant code to your game each night, instead of, you know... _procrastinating_.
* **Commit early, commit often.** Don’t be afraid to break something because you can always go back in time to a previous version.
* **Consult documentation resources** (MDN, jQuery, etc.) at home to better understand what you’ll be getting into.
* **Don’t be afraid to write code that you know you will have to remove later.** Create temporary elements (buttons, links, etc) that trigger events if real data is not available. For example, if you’re trying to figure out how to change some text when the game is over but you haven’t solved the win/lose game logic, you can create a button to simulate that until then.

---

### Potential Project Ideas

##### Blackjack
Make a one player game where people down on their luck can lose all their money by guessing which card the computer will deal next!

##### Concentration
Sometimes just called "Memory", it's a card game in which all of the cards are laid face down on a surface and two cards are flipped face up over each turn. If you get all the matching cards, you've won!

##### Self-scoring Trivia
Test your wits & knowledge with whatever-the-heck you know about (so you can actually win). Guess answers, have the computer tell you how right you are!

---

### Useful Resources

* **[Github Pages](https://pages.github.com)** _(for hosting your game)_
* **[MDN Javascript Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)** _(a great reference for all things Vanilla Javascript)_
* **[jQuery Docs](http://api.jquery.com)** _(if you're using jQuery)_
* **[Skeleton](https://webdesign.tutsplus.com/tutorials/building-html-page-structure-with-skeleton--cms-23253)** *(Good tutorial on how to build pages with Skeleton)*
* **[Coolors](https://coolors.co/)** *(Easy palette generator)*
* **[Flat Colors](http://flatcolors.net/palettes.php)** *(Flat color palettes)*

---



