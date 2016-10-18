# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project #2: Building & consuming your own API

## Project Submission
1. Push your front-end repo to Github Pages and back-end repo to Heroku.
2. Ensure that a soft launch of your project is up on Github Pages and Heroku by Wednesday 26th October 2016.
3. Submit the links at the **Project 2 submission page**
4. The deadline for this project is on Friday 28th October 2016, 8am
5. Before the deadline ensure that the master branch contains your latest project code. (There is no need to have a gh-pages branch)
6. Before the deadline ensure that your apps are successfully deployed to Heroku

### Overview

This second project is your first foray into **building a full-stack application.** You'll be **building a Node app** which serves an API and a **front-end application** which consumes the API.

**This is exciting!** It sounds like a lot, but you already have all the tools to build them! Get creative in choosing what sort of application you want to build!

**You will be working individually for this project**, and you'll be designing the app yourself. We hope you'll exercise creativity on this project, sketch some wireframes before you start, and write user stories to define what your users will want to do with the app. Make sure you have time to run these ideas by your instructors to get their feedback before you dive too deep into code! Remember to keep things small and focus on mastering the fundamentals – scope creep/feature creep is the biggest pitfall for any project!

### Project 2A: Blog
Develop a blog with the below minimum technical requirements.

### Project 2B: Freestyle App
Develop your own personal project with the below minimum technical requirements.

### Technical Requirements

Deliverables include:
* **Node back-end server**
  * Preferably with **Mongoose** and **Express**
  * API should be created using **at least 3 related models** ( more if they make sense )
  * Generate views using **templates**
    * Project 2A, your models should be:
      * User - someone using your application
      * Post - blog posts
      * Comment - comments on the posts.
    * Project 2B:
      * one user model
      * remaining models - depending on functional idea
  * Include **all major CRUD functions** in a **RESTful API** for at least one of those models
* **Front-end application**
  * Consume **your own API** with **AJAX** calls to the back-end server
  * Layout and style your front-end with **clean & well-formatted CSS**
* **Overall**
  * Craft thoughtful user stories
  * **ER** and **user flow diagrams**
  * **Deploy your application online** so it's publicly accessible

Optional
* **Include sign up/log in functionality**, with encrypted passwords and an authorization flow  
* Incorporate external APIs
  * Consumed by your front-end application
  * Consumed by your back-end application in the models
  * Feel free to utilize and combine a few external APIs to create a more useful API

---

## Presentation format
* Presentations are 8 mins: 5 mins presentation and 3 mins feedback/Q&A
* Students to present on one project (Either project 2A or 2B)
* The order of the presentation will be random.
* Student before the current presenter to give feedback in the form of one glow comment (One great thing about their project)
* Student after the current presenter to give feedback in the form of one grow comment (A possible improvement to their project)

###Things to mention during your presentation:
* Explain what your app is about and demo it
* Talk about your planning process
* Show your code
* Explain how you organized your codes
* Share interesting code solutions
* Talk about any issues you encountered during the project and how you overcame them.

### Project Feedback + Evaluation

* __Project Workflow__: Did you complete the user stories, wireframes, task tracking, and/or ERDs, as specified above? Did you use source control as expected for the phase of the program you’re in (detailed above)?

* __Technical Requirements__: Did you deliver a project that met all the technical requirements? Given what the class has covered so far, did you build something that was reasonably complex?

* __Creativity__: Did you add a personal spin or creative element to your project submission? Did you deliver something of value to the end user (not just a login button and an index page)?

* __Code Quality__: Did you follow code style guidance and best practices covered in class, such as spacing, modularity, and semantic naming? Did you comment your code as your instructors have in class?

* __Deployment and Functionality__: Is your application deployed and functional at a public URL? Is your application free of errors and incomplete functionality?

* __Total__: Your instructors will give you a total score on your project between:

| Score| Expectations |
| :----:| :---------: |
| **0** | _Incomplete._ |
| **1** | _Does not meet expectations._ |
| **2** | _Meets expectations, good job!_ |
| **3** | _Exceeds expectations, you wonderful creature, you!_ |

 This will serve as a helpful overall gauge of whether you met the project goals, but __the more important scores are the individual ones__ above, which can help you identify where to focus your efforts for the next project!

---

### Necessary Deliverables

* Github Repo 1: A **working API**, hosted on Heroku
* Github Repo 2: A front-end that **consumes your own API**, hosted on Heroku or Github Pages.
* A **link to your hosted working app** in the URL section of your GitHub repos
* **A ``readme.md`` file** with:
    * Explanations of the **technologies** used
    * A couple paragraphs about the **general approach you took**
    * **Installation instructions** for any dependencies
    * Link to your **user stories** – who are your users, what do they want, and why?
    * Link to your **wireframes** – sketches of major views / interfaces in your application
    * Link to your **diagrams** – ER and user flow diagram
    * Descriptions of any **unsolved problems** or **major hurdles** your team had to overcome

---

### Suggested Ways to Get Started

* **Begin with the end in mind.** Know where you want to go by planning with wireframes & user stories, so you don't waste time building things you don't need
* **Don’t hesitate to write throwaway code to solve short term problems**
* **Read the docs for whatever technologies you use.** Most of the time, there is a tutorial that you can follow, but not always, and learning to read documentation is crucial to your success as a developer
* **Commit early, commit often.** Don’t be afraid to break something because you can always go back in time to a previous version.
* **User stories define what a specific type of user wants to accomplish with your application**. It's tempting to just make them _to-do lists_ for what needs to get done, but if you keep them small & focused on what a user cares about from their perspective, it'll help you know what to build
* **Write pseudocode before you write actual code.** Thinking through the logic of something helps.

---

### Potential Project Ideas

##### Cheerups
The world is a depressing place.

Your task is to create an app that will allow people to create and share "cheerups" - happy little quips to brighten other people's' days. Cheerups will be small - limited to 139 characters. Members will be able to promote Cheerups that they like and maybe even boost the reputation of the Cheerupper.

##### Bookmarket
You will create an application where users can bookmark links they want to keep.

But what if users could trade bookmarks for other bookmarks? Or sell bookmarks for points? Or send bookmarks to your friends. Or something even crazier.

##### Photo sharing app
Users will be able to register and create albums and photos. Albums and photos will need to be named and described by their owners. Users will be able to view other user's' albums. Maybe users can comment on photos, or either up/down vote them.

---

### Useful Resources

* **[Heroku](http://www.heroku.com)** _(for hosting your back-end)_
* **[Writing Good User Stories](http://www.mariaemerson.com/user-stories/)** _(for a few user story tips)_
* **[Presenting Information Architecture](http://webstyleguide.com/wsg3/3-information-architecture/4-presenting-information.html)** _(for more insight into wireframing)_
