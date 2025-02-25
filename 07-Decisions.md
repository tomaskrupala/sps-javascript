# Decisions

Without decisions the code would be too straight forward to be really useful.

## If, Else

Basic construction for deciding flow of the program. Executes blocks of commands based on condition.

Let's start with a simple example:

    //script execution

    //Can I buy this item in a shop?
    let doIHaveEnoughMoney = true;

    if (doIHaveEnoughMoney) {
        console.log("I can buy this!");
    }

    console.log("Leaving shop");

After `if` keyword we will have a condition inside of `()` and if it is evaluated to `true` then block after it **will** be executed. Otherwise it will **not**.

In case we need to execute specific code for condition evaluated to `false` we can write code in example bellow.

    //script execution

    //Can I legally drink alcohol in Czech Republic?
    const legalDrinkingAge = 18;
    let myAge = 17;

    if (myAge >= legalDrinkingAge) {
        console.log("Yes, I can!");
    } else {
        console.log("No, I can't!");
    }

Which is using `else` block. Which will be executed in case of condition being evaluated to `false`. This block is optional.

And for more complicated decisions we can even daisy chain `if else` statements. Creating for example:

    //script execution

    //What highest possible fireworks category can I buy?
    let myAge = 40;
    let haveFireworksLicense = true;

    let fireworksCategory;

    if (haveFireworksLicense) {
        fireworksCategory = "F4";
    } else if (myAge >= 21) {
        fireworksCategory = "F3";
    } else if (myAge >= 18) {
        fireworksCategory = "F2";
    } else if (myAge >= 15) {
        fireworksCategory = "F1";
    } else {
        fireworksCategory = "None";
    }

    console.log("I can buy fireworks of category:", fireworksCategory);

Here we are using `else if` condition which is basically `else` block which contains new `if` statement.

Order of statements matter! When condition is evaluated to `true` no other block will be checked.

Note: Daisy chaining is powerful but with many blocks it can get hard to read and maintain. I would recommend not using it for more then 5 blocks.

Note: It is good practice to always include `else` block for daisy chaining so we have certainty that execution just did not fall through. In example above we are using the `else` block for catching case when we can't buy fireworks.

## AND, OR, NOT

Of course we can use more than one condition inside of `if`. We can join these conditions by using **AND** or **OR** and we can negate it by using **NOT**.

But these don't have to be used only in conditions. But that is place where these are used mostly.

### AND

Joining conditions via **AND** written as `&&` (2x ampersand) means that **all** parts needs to be evaluated to `true` for condition to be `true`. Otherwise it is evaluated as `false`.

    //script execution

    //Can I ride the rollercoaster?
    const minAge = 12;
    const minHeight = 140;

    let height = 120;
    let age = 15;

    if (height >= minHeight && age >= minAge) {
        console.log("You can ride the rollercoaster!");
    } else {
        console.log("Sorry, you can't ride the rollercoaster");
    }

Of course it is possible to join more then two conditions.

### OR

Joining conditions via **OR** written as `||` (2x pipe) means that **at least one** part needs to be evaluated to `true` for condition to be `true`. Otherwise it is evaluated as `false`.

    //script execution

    //Do we have a beer at home?
    let beerInsideFridge = true;
    let beerInsideCupboard = true;
    let beerInsideBasement = true;

    if (beerInsideFridge || beerInsideCupboard || beerInsideBasement) {
        console.log("We have some beer at home!");
    } else {
        console.log("Time to go shopping!");
    }

### NOT

**NOT** is unary operator which can be used to reverse **boolean** value or condition and it is written as `!` (exclamation mark).

    //script execution

    //Light switch
    let lightSwitchIsOn = false;

    console.log("Light is on: " + lightSwitchIsOn);

    //Toggle the light switch
    lightSwitchIsOn = !lightSwitchIsOn;

    console.log("Light is on: " + lightSwitchIsOn);

    //Toggle the light switch
    lightSwitchIsOn = !lightSwitchIsOn;

    console.log("Light is on: " + lightSwitchIsOn);

It is mostly beneficial in shortening `if` statements. We can rewrite:

    //script execution

    //Can I sleep longer?
    const haveToGoToWork = true;

    if (haveToGoToWork) {
        //wake up...
    } else {
        console.log("I can sleep longer!");
    }

To simpler code:

    //script execution

    //Can I sleep longer?
    const haveToGoToWork = true;

    if (!haveToGoToWork) {
        console.log("I can sleep longer!");
    }

## Switch

A `switch` statements allows to evaluated an expression and then match it against `case` labels. When match is found engine will execute associated block with that label, till it finds `return` or `break` statement, this allows for **case fallthrough**.

    //script execution

    //Asian grading scale
    let grade = "B";

    switch (grade) {
        case "A":
            console.log("Average");
            break;
        case "B":
            console.log("Bellow Average");
            break;
        case "C":
            console.log("Can't eat dinner");
            break;
        case "D":
            console.log("Don't come home");
            break;
        case "F":
            console.log("Find a new family");
            break;
        default:
            console.log("Invalid grade");
            break;
    }

In example above we also have a `default` label which catches case when no label is matched for evaluated expression.

Note: It is good practice to always include `default` block so we have certainty that execution was not skipped because no label was matched.

Note: **Case fallthrough** is powerful tool but it can lead to unexpected behavior. And it is not recommended and many static generators warn against it.

## Ternary operator

In **Javascript** there is ternary operator (ternary means it has three required parts) which is written via `?` (question mark) `:` (colon). Specifically `condition ? action_on_true : action_on_false` which will base on **condition** evaluation executes one of two actions. In case that evaluation is `true` action between `?` and `:` will be executed. Otherwise action after `:` will be executed.

    //script execution

    //How was lunch?
    let delicious = false;

    console.log("How was lunch?", delicious ? "Delicious!" : "Barely edible!");
