# **Features**

**This uses Cucumber's [Gherkin syntax](https://cucumber.io/docs/gherkin/reference/) and it is advised that you check out information around this from them directly.**

The [example feature](cucumber_features/example.feature) shows examples of how a feature file can be constructed. This uses the `Feature, Scenario, Given, When, Then` syntax.

```gherkin
Feature: Google Search

I want Google search to function as expected with user input

Scenario: Get a search results value back from Google
    Given I enter 'hello world' into the search bar
    When I search in Google
    Then I get a list of search results returned
```

The [example feature](cucumber_features/example.feature) shows 2 different scenario types that are used frequently.

Each step is mapped to a corresponding step definition found in the [corresponding directory](step_definitions). Explanations of the code are listed in the examples. This is not an extensive list and should be used as examples for construction of step definitions for further expansion to suit your needs - see [oTTo Cheatsheet](../docs/cheatsheets/otto_hints_and_tips.md) for hints and tips

As long as the parent directory is called `cucumber_features` then Cucumber will recursively scan the folder for any/all feature files so you can store then in easy to organise folders within the parent directory.

There are 3 `tags` in the example feature file - `@tag1`, `@tag2` and `@single_test_tag`. These can be used to label feature files for complete runs alongside other feature files that are tagged in the same way (`@tag1` and `@tag2`) as well as individual tests been labeled so test cases can be run in isolation or smaller subsets (`@single_test_tag`). These tags will apply across all feature files within the parent directory.

The support folder stores a variety of things that are crucial to the operation of oTTo and some things that are helpful. Below is a list of the simpler ones that you should not need to edit regularly:

- **app.rb** creates a SitePrism subclass to allow [snake case](https://en.wikipedia.org/wiki/Snake_case) writing of page modules i.e. test_divs.element instead of TestDivs.element
- **browser_drivers.rb** definitions of the different browser drivers that oTTo is capable of using with Selenium. To be used in [runtime script](scripts/test.sh)
- **multiple_assertions.rb** RSpec extensions to allow checking of multiple extension in one step without escaping code block at initial step if failures are found

The following are files that might need editing as your usage of oTTo increases:

- **hooks.rb** a handy place for storing any Cucumber `Before` or `After` hooks. This might have limited usage for you these can also be described in the `env.rb`
- **env.rb** this is the engine block of oTTo defining load paths, required gems, supporting files within the project, user defined modules as well as startup information for oTTo's underlying tech (Capybara, SimpleCov etc). **NOTE** _make sure you update this with any new modules otherwise you will not have them included in your code for use!!_

## **Useful tips**

- When your feature files have grown in number as your test suite matures, during development try using the `@test` single tag to only run one (or a couple) of scenarios at a time. This reduces the waiting time for each run to finish if you only care about developing one scenario.
