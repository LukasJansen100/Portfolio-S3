# Software Quality
*You use software tooling and methodology that continuously monitors and improve the software quality during software development.*

## Code Reviews
>Code review (sometimes referred to as peer review) is a software quality assurance activity in which one or several people check a program mainly by viewing and reading parts of its source code, and they do so after implementation or as an interruption of implementation. At least one of the persons must not be the code's author. The persons performing the checking, excluding the author, are called "reviewers".
[Wikipedia on Code review](https://en.wikipedia.org/wiki/Code_review)

In both the Individual and Group project Code Reviews are used for reasons mentioned above.
In the group project we have a "repository rule" where at least 2 people must have reviewed and approved your code before it can be merged into the developement or main branch.

For the individual project it's a bit harder to do code reviews because Teun and I write code together most of the time, this means we are both authors, thus technically can't also call ourselfs reviewers. Still we have a repository rule where the both of us must approve changes when merging into the main branch. 

## Unit Testing
>In computer programming, unit testing is a software testing method by which individual units of source code—sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures—are tested to determine whether they are fit for use.
[Wikipedia on Unit testing](https://en.wikipedia.org/wiki/Unit_testing)

In the group project unit testing plays an important role. On our projects we strive for a high code coverage, this means that for the parts of our code that we think are vulnerable, should be tested. The Unit Tests also play a role in the CI/CD of the projects. Whenever new changes are made on branches and pushed to the repository, the CI/CD runs all the unit tests.
