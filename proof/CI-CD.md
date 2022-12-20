# CI/CD
*You design and implement a (semi)automated software release process that matches the needs of the project context.*

# What is CI/CD?
> In software engineering, CI/CD or CICD is the combined practices of continuous integration (CI) and (more often) continuous delivery or (less often) continuous deployment (CD). [Wikipedia CI/CD](https://en.wikipedia.org/wiki/CI/CD)

![CICD Image](https://user-images.githubusercontent.com/93530655/199507551-dc179c00-2907-4b91-bdb2-671c3baf4c51.png)


# Implementation Individual Project

## CI
To Continuously Integrate new code into our project, we use different branches. When we want to add a new feature, or fix a problem, we create a branch (more information about branches [here](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)). Once we have finished the new feature or fixed the problem, we can merge the branch into the "Main Branch".

Because we don't wany any problems on the main branch, the CI pipeline made with github actions automatically builds the project, to see if it can sucessfully run. Additionally, repositories that have integration tests and unit tests, will also automatically run these tests.


After pushing a branch or merging, SonarCloud will give a report on the code quality and test coverage. [Click here](https://sonarcloud.io/organizations/ips3-db04-teun-mos-lukas-jansen/projects) to see projects on SonarCloud.
SonarCloud is a tool that gives a static code analysis over the code you've written, and it can also show your code coverage over a project. Read more about [SonarCloud here](https://docs.sonarcloud.io/).

## CD
To continuously deliver our projects we use [Docker](https://docs.docker.com/get-started/). After a successful merge into main, the CD pipeline creates a docker image from the main branch, and publishes it on [Dockerhub](https://hub.docker.com/u/teunlukas).

Other people can pull our docker images from dockerhub.
With docker compose, you can easily pull all the docker images, and simultaneously run them. you can find more information about docker compose on our [main page](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen).

# Implementation Group Project
The group project also has a relatively similar CI/CD.
Including automated building, and testing. Static Code Analysis by SonarCloud. Pushing merges to main to [Dockerhub](https://hub.docker.com/r/judahlit/modus-1/tags)

[Judah](https://github.com/judahlit) our Git Master, and has set up the CI/CD in the group project.
