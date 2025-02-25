# Loops

Loops can be used to execute same code multiple times or. Either to do same thing or similar thing thanks to change in variable values.

There are two distinct ways how to loop either till something happens for that we have **while** construct or loop X number of times for that we have **for** construct.

## While

While loop is most universal loop available in Javascript. It can be used in any situation requiring looping, though other loops may be better suited.

Main usage of while loop is do something until something happens.

Standard while loop syntax looks like:

    while (condition) {
        // code to run

        //update condition or break
    }

`while` keyword defines we will be using **while** loop. `condition` is either bool variable or expression resulting in bool value. Which defines if code inside of loop should be executed.

Every loop needs to have a way to update values used in `condition` so that loop can exit. Or it needs to have direct exit via `break` statement.

There is simple example: We have test which can be passed when score is more than 90 points, every test score is given on random (between 0 and 100 points) and we want to know how many tries it took. Given that this is using random it will produce different values every time. This variant is using setting **loop condition** to `false` to exit loop.

    // script execution

    // returns random integer between 0 and max (exclusive)
    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    const requiredPointsToSucceed = 90;

    let passed = false;
    let tries = 0;

    while (!passed) {
        tries++;

        const points = getRandomInt(101);

        console.log(`Try ${tries}: ${points} points`);

        if (points >= requiredPointsToSucceed) {
            passed = true;
        }
    }

    console.log(`You passed after ${tries} tries congratulation!`);

Variant of script from above which is using `break` statement to exit loop.

    // script execution

    // returns random integer between 0 and max (exclusive)
    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    const requiredPointsToSucceed = 90;

    let tries = 0;

    while (true) {
        tries++;

        const points = getRandomInt(101);

        console.log(`Try ${tries}: ${points} points`);

        if (points >= requiredPointsToSucceed) {
            break;
        }
    }

    console.log(`You passed after ${tries} tries congratulation!`);

### Do while variant

Is specialized variant which ensures that code is executed at least once before condition is checked.

Rewritten example from above as do-while.

    // script execution

    // returns random integer between 0 and max (exclusive)
    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    // do-while loop
    const requiredPointsToSucceed = 90;

    let passed = false;
    let tries = 0;

    do {
        tries++;

        const points = getRandomInt(101);

        console.log(`Try ${tries}: ${points} points`);

        if (points >= requiredPointsToSucceed) {
            passed = true;
        }
    } while (!passed);

    console.log(`You passed after ${tries} tries congratulation!`);

## For

For loop is loop which is used mostly in situations when we know how many times we need to execute it.

Standard for loop syntax looks like:

    for (initializer; condition; final-expression) {
        // code to run
    }

`for` keyword defines we will be using **for** loop. Different parts of loop definition are separated by `;` (semicolon) and are optional. `initializer` is mostly number type variable defining how many times loop already run it is called **counter variable**. `condition` expression resulting in bool value which defines if loop should run. `final-expression` is always evaluated when loop finishes iteration and is used to update **counter variable**.

There is simple example: We need to grade all test.

    // script execution

    // returns random integer between 0 and max (exclusive)
    function getRandomInt(max) {
        return Math.floor(Math.random() * max);
    }

    // for loop
    const testToGrade = 26;

    for (let i = 0; i < testToGrade; i++) {
        console.log("Test graded, points:", getRandomInt(101));
    }

    console.log("All test have been graded!");

## Looping through collections

Collections are often used in loops to traverse data they are holding. Loops such as **for** can be used for this activity but there are specialized loops like **for...of** which are better.

Example of standard **for** loop: Writing out names of EU countries from array capitalized.

    // script execution

    const euCountriesArray = [
        "Germany",
        "France",
        "Italy",
        "Spain",
        "Poland",
        "Netherlands",
        "Belgium",
        "Greece",
    ];

    for (let i = 0; i < euCountriesArray.length; i++) {
        console.log(euCountriesArray[i].toUpperCase());
    }

### For...of

Standard **for...of** loop syntax looks like:

    for (const variable of collection) {
        // code to run
    }

`for` keyword defines we will be using **for** loop in this case specialized version. `variable` is place for current value from collection. `collection` defines which collection we are traversing.

This way we can work with individual values from array, but not modify content of array itself. For that reason we are working with values as **constants**.

Example from above rewritten as **for...of**:

    // script execution

    const euCountriesArray = [
        "Germany",
        "France",
        "Italy",
        "Spain",
        "Poland",
        "Netherlands",
        "Belgium",
        "Greece",
    ];

    for (const country of euCountriesArray) {
        console.log(country.toUpperCase());
    }

### ForEach

ForEach function allows to use provided function for each member of collection.

Standard **forEach** syntax looks like:

    collection.forEach(function);

`collection` represents collection we want to traverse. `function` represents function which will be executed for every item in collection.

Note: `forEach` function may take more then one parameter. Their definition, optionality and values are dependent on underlying collection.

Example: Logging each member of collection.

    // script execution

    // function will log provided variable
    function justLog(string) {
        return console.log(string);
    }

    const euCountriesArray = [
        "Germany",
        "France",
        "Italy",
        "Spain",
        "Poland",
        "Netherlands",
        "Belgium",
        "Greece",
    ];
    console.log(euCountriesArray);

    euCountriesArray.forEach(justLog);

### Map

Map function is available only for **array** collection and allows us to modify each item and create a new array collection of these modified items.

Standard **map** syntax looks like:

    const newCollection = collection.map(function);

`collection` represents **array** collection we want to traverse. `function` represents function which will be executed for every item in collection. `newCollection` represents newly created **array** collection from collection with modified items.

Example: Creating collection of EU country names with capitalized letters from collection of EU country names with standard capitalization.

    // script execution

    // function which will uppercase a string
    function toUpperCase(string) {
        return string.toUpperCase();
    }

    const euCountriesArray = [
        "Germany",
        "France",
        "Italy",
        "Spain",
        "Poland",
        "Netherlands",
        "Belgium",
        "Greece",
    ];
    console.log(euCountriesArray);

    const euCountriesUpper = euCountriesArray.map(toUpperCase);
    console.log(euCountriesUpper);

### Filter

Filter function is available only for **array** collection and allows us to test each item against filter function and create a new **array** collection of items that passed.

Standard **filter** syntax looks like:

    const newCollection = collection.filter(function);

`collection` represents **array** collection we want to traverse. `function` represents function which will be executed for every item in collection testing them, this function **must return boolean value**. `newCollection` represents newly created **array** collection from items which passed filter test.

Example: Creating collection of EU country names which are shorter or equal to 6 characters from collection of EU country names.

    // script execution

    // function which will return bool on condition string is shorter or equal to 6 characters
    function hasShortName(string) {
        return string.length <= 6;
    }

    const euCountriesArray = [
        "Germany",
        "France",
        "Italy",
        "Spain",
        "Poland",
        "Netherlands",
        "Belgium",
        "Greece",
    ];
    console.log(euCountriesArray);

    const euCountriesWithShortNames = euCountriesArray.filter(hasShortName);
    console.log(euCountriesWithShortNames);

Note: We can combine usage of functions on **array** collections. Order of functions matter.
