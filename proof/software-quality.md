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

### Unit Testing in Group Project
In the group project unit testing plays an important role. On our projects we strive for a high code coverage, this means that for the parts of our code that we think are vulnerable, should be tested. The Unit Tests also play a role in the CI/CD of the projects. Whenever new changes are made on branches and pushed to the repository, the CI/CD runs all the unit tests.

### Unit Testing in Individual Project
We have made Unit Tests on the User-Preferences-API, these unit tests, test whether the API calls return the correct information, we do this by mocking our database with [MongoMock](https://github.com/mongomock/mongomock), and we test using the [PyTest framework](https://docs.pytest.org/).

Unit tests are automatically run in the [build and test workflow](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen/User-Preferences-API/blob/main/.github/workflows/build-and-test.yml) of the User-Preferences-API

## Integration Testing
Integration testing is a way to test if the different modules in your application work together as intended. It occurs after unit testing and before system testing.
Integration tests use actual components that the app uses in production, requires more code and data processing and takes longer to run. Therefore if you have behaviour that can be tested with unit tests or integration tests, always choose unit tests. ([ASP.NET introduction to integration tests](https://learn.microsoft.com/en-us/aspnet/core/test/integration-tests?view=aspnetcore-7.0))

### Integration Testing in individual project
In the individual project we have made integration tests, to test the integration between the "Integration-API" and the Frontend.
The integration tests are setup to test the actual endpoints which the frontend calls. To test these endpoints, we've mocked the data-access-layer and the authentication needed to call the endpoints.
[Click here](https://github.com/IPS3-DB04-Teun-Mos-Lukas-Jansen/Integration-API/tree/main/Integration-API/Integration-API.Integration-tests) to view the integration tests we've made on the "Integration-API".
