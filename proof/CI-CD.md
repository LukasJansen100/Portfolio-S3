# CI/CD
*You design and implement a (semi)automated software release process that matches the needs of the project context.*

# What is CI/CD?
> In software engineering, CI/CD or CICD is the combined practices of continuous integration (CI) and (more often) continuous delivery or (less often) continuous deployment (CD). [Wikipedia CI/CD](https://en.wikipedia.org/wiki/CI/CD)

![CICD Image](https://user-images.githubusercontent.com/93530655/199507551-dc179c00-2907-4b91-bdb2-671c3baf4c51.png)


# Implementation Individual Project
In our individual project, [Teun](https://github.com/TeunMos) and I store the code of our projects in our [repositories](https://github.com/orgs/IPS3-DB04-Teun-Mos-Lukas-Jansen/repositories) on github. 

## CI
To Continuously Integrate new code into our project, we use different branches. When we want to add a new feature, or fix a problem, we create a branch (more information about branches [here](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)). Once we have finished the new feature of fixed the problem, we can merge the branch into the "Main Branch".

Because we don't wany any problems on the main branch, the CI pipeline made with github actions automatically builds the project, to see if it can sucessfully run.

Currently we haven't implemented any automated testing, once we start making unit tests, we also want the CI pipeline to run all the tests, then if all are successful, you can merge your branch into main.

## CD
To continuously deliver our projects we use [Docker](https://docs.docker.com/get-started/). After a successful merge into main, the CD pipeline creates a docker image, and publishes it on [Dockerhub](https://hub.docker.com/).


# Implementation Group Project
