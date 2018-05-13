Running PHPUnit test:

There are different ways by which we can run our PHPUnit Tests. Either run a full unit test, a test suite or one specific test as shown in following commands:-

To run all the tests available from the custom modules directory:-
vendor/bin/phpunit -c core/phpunit.xml.dist modules/custom

Here, phpunit.xml.dist is the configuration file for PHPUnit. This holds various attributes like bootstrap, color etc. which helps PHPUnit to perform tests.

To run all tests(Unit, Kernel, Functional) from particular module:-
vendor/bin/phpunit -c core/phpunit.xml.dist modules/custom/phpunit_example

To run only all Unit tests from a specific module:-
vendor/bin/phpunit -c core/phpunit.xml.dist modules/custom/phpunit_example/tests/src/Unit

To run a specific UnitTest:-
vendor/bin/phpunit -c core/phpunit.xml.dist modules/custom/phpunit_example/tests/src/Unit/UnitTest.php

To run a specific group test:-
vendor/bin/phpunit -c core/phpunit.xml.dist modules/custom --group phpunit_example

Setting up our own PHPUnit.xml

We can have our own php-unit.xml where we specify the tests which we intend to run. To achieve this copy the core/php-unit.xml.dist file and paste into the root folder of your project and replace it’s content by following:

<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="core/tests/bootstrap.php" colors="true">
  <testsuites>
    <testsuite name="unit">
      <directory>modules/custom/phpunit_example/tests</directory>
    </testsuite>
  </testsuites>
</phpunit>


Now run vendor/bin/phpunit and that’s it.

This is very simple configuration file, but it sets two important properties: <directory>modules/custom/phpunit_example/tests</directory> tells PHPUnit where your tests will be located, and colors="true" makes sure your test results are in color. So everytime we run our tests, we don’t need to specify them explicitly, cool.
There are other attributes as well, but I have used only two of those for this example, you can explore them in your project.


Testsuite:
<testsuite name="unit">
      <directory>modules/custom/phpunit_example/tests</directory>
</testsuite>
In our example, we have created a test-suite unit, in php-unit.xml.dist and to run a specific test-suite run the following command:
vendor/bin/phpunit --testsuite unit
