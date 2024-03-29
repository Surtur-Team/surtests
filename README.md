# Surtests

A testing framework for C using the surtur build tool. This was originally built for the surtur build tool but can be used without it as well.

# Documentation

**IMPORTANT: This was only tested on linux, so no gurantee for Windows and macOS support**

## Creating your tests

> For an example look at: [Example](src/main.c)

First we need to include "tests.h". **(This does not work yet since dependencies are not done. If you still want to use this, copy the code into your own project)**

Then in our function (the main function in the example but any funtion works) we need to call TEST(...)

The arguments for this are: TEST(the_name_for_my_test, { }).

The **first** arg is an identifier that describes the name of your test, for example: my_test or the_name_for_my_test.

The **second** arg is a block that will be executed. Here you can do all your testing related logic like assertions:
```c
TEST(my_test, {
  ASSERT(100 == 10);
});
```

In this snippet, we use the ASSERT macro from tests.h to check if a condition evalutes to true. Otherwise it will throw an error.

Another useful feature is disabling your tests. This is particularly useful when running more than one test.

To do so you can add an exclamanation mark in front of the name: TEST(!my_test, { })

## Running your tests

**If you use surtur you can simply do:**

`surtur test <NAME>`. Note that the <NAME> arg is not required and not providing it will just run all tests.

If you do provide the test name for example `my_test` (`TEST(my_test, {})`), it will only run that test. You can also provide multiple by seperating them with a comma.

Run all tests: `surtur test`
Run one test: `surtur test my_test` (replace my_test with the actual test name)
Run multiple tests: `surtur test my_test,your_test,his_test` (The names are seperated by a comma. Do NOT use whitespace here)

**If you don't use surtur**:

Tests will be enabled by default, but can be disabled with -DNOTESTS
Example with gcc:
`gcc main.c -DNOTESTS -o main`

When you do use tests however, you need to specify which ones should be ran.

Before executing your code you need to specify the tests that should be run. Not doing so will run all tests.
Do this by running `export SURTUR_TESTS="my_test"` or multiple with `export SURTUR_TESTS="my_test,your_test"` (**NOTE: "Export" only works on unix-like systems**)

After this you can do:
`./main`

And the specified tests should be ran.
