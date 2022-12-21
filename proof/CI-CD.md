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

<details>
  <summary>Example CI workflow (used in User-Preferences-API)</summary>
  
  ``` yml
  # This workflow will build a .NET project
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-net

name: .NET

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: 6.0.x
    - name: Restore dependencies
      working-directory: ./Integration-API
      run: dotnet restore
    - name: Build
      working-directory: ./Integration-API
      run: dotnet build --no-restore
    - name: Test
      working-directory: ./Integration-API
      run: dotnet test --no-build --verbosity normal
  ```


</details>


## CD
To continuously deliver our projects we use [Docker](https://docs.docker.com/get-started/). After a successful merge into main, the CD pipeline creates a docker image from the main branch, and publishes it on [Dockerhub](https://hub.docker.com/u/teunlukas).

Other people can pull our docker images from dockerhub.
With docker compose, you can easily pull all the docker images, and simultaneously run them. you can find more information about docker compose on our [main page](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen).

<details>
  <summary>Example CD workflow (used in User-Preferences-API)</summary>
  
  ``` yml
name: Docker Image CI

on:
  pull_request:
    branches: [ "main" ]
  push:
    branches: [main]

jobs:

  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["3.11"]


    steps:
    - uses: actions/checkout@v3
    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v4
      with:
        python-version: ${{ matrix.python-version }}
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest
        pip install -r requirements.txt
    - name: Lint with flake8
      run: |
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    - name: Test with pytest
      run: |
        pytest -v
  
  sonarcloud:
    name: SonarCloud
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - name: Setup Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: | 
          python -m pip install --upgrade pip
          pip install pytest coverage
          pip install -r requirements.txt
      - name: Run coverage check
        run: |
          coverage run -m pytest
          coverage xml
      - name: SonarCloud Scan
        uses: SonarSource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
  ```
</details>

### Deployment research
You can find a research paper about the deployment of Monkodash [over here](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen/Documentation/blob/main/ResearchDocuments.md).

# Implementation Group Project
The group project also has a relatively similar CI/CD.
Including automated building, and testing. Static Code Analysis by SonarCloud. Pushing docker images from merges into main to [Dockerhub](https://hub.docker.com/r/judahlit/modus-1/tags)

