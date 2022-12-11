Booking Controller:

FILE: BookingController.php

Ups:

    .Does its job
    .It's easy to read since it shows every drop of action
    .In some parts the code is very straight forward
    .There is programming patterns in the code which makes it organized

Downs:

    .Repeated code in a none usefull way
    .Some syntax is wrong
    .The code is checking for ADMIN Tokens in a .env file which I believe to be a none correct way of handling this. (I hope I am not misunderstanding the logic here)
    .Some of the statements are being handled in a "drop by drop way" (it has too many steps, we can do the same in a simpler and faster way)



Thoughts and concerns:

In the function "index(Request $request)"" I saw that the api will check for the type of id a client is using, everything is fine with that, but the way is doing it I believe to be wrong and insecure, getting an ADMIN_ID from an .env file can be dangerous since it's hardcoded, if any vulnerabilty that gives the attacker the possibility of reading system files he will have access to those ADMIN token's and we already know how the story will end.

So in order to prevent that, if it's really necessary to have those tokens hardcoded without any time limit, we should explore new applications to store tokens like "Secret Manager" by Google Cloud.


////

The Controller uses __authenticatedUser to check for the current authenticated user type, I believe a more correct way of doing this would it be by calling Auth::id() to a variable and using it during the code session, so we avoid unnecessarily calling the same method over and over again.

Ex:

    $auth_user = Auth::id();

We can do the same when we call a "$request", we could simply say  "$request = user()""

////

Some IF statements have too many conditions (I marked it as "IF STATEMENT PROB" in the code), there is no need for 2 conditions, the isset() function will already make that job for us, and it's ok too take out the else as well, we see that the else sets the value to ' "" ' if the value of the requested field is ' "" ' but that's useless in my prespective since the request value is already ' "" ' the variable value will be ' "" ' already. (I hope I made it easy to understand, I commented the code so you could have a foothold)

////

I marked a comment saying "RETURN" in the code because it was using an expression to simplify an if statement:  

-> if(stuff) return something;

If the statement only has one condition, I believe that's good because makes the code simple and it's a good practice, but ONLY if we do that since the biggining of the code, otherwise it will look like the code was written by 2 diferent people which can create some confusion in the workplace, since we are working as a team I belive the best practice should be adapt to the way the code is already written (unless obviously it's a complete chaos).


Overall Review:

The code itself is good, it's built in ways that makes it easier for the developer to find out what the code is doing and easly refactor it if needed, but, on the other hand, it has a lot of unecessary lines and conditions that once removed or changed would make the code ligther, faster, and more polished to other developers working on the same project.

I would compare this code to a plate of my favourite food that looks very appetizing, but as soon as I dig into it I find a piece of hair hiding there...still appetizing, but I'll send it back for a "refactoring".





Booking Repository:

FILE: BookingRepository.php

Pros:

    .This code has a lot of things that in one hand there is no need for them to be there, but on the other makes the code more readable and easy to understand
    .It is very well composed
    .Always follows the same structure
    .Functions do one thing and they do it well

Cons:

    .In some parts of the code statements don't follow the same patterns as the codeblock does
    .There is too many stuff that could be sent into functions to organize the code better
    .The code has some unuseful steps


Thougths and concerns:

The isset() function can have multiple parameters, so instead of repeating it we can simple do:

-> isset(param1, param2)

And we will get the same answer, it's faster and easier to read.

////

I marked a comment as "CODE BLOCKS":

Here we can see too much code being repeated, it would be easier if we created a function inside the class to handle those errors, we would be sparing time, code lines, and neurons.

By doing this we will as well let the next developer in a more confortable position while reading and creating new code.

////

I marked a comment as "GOOD ONE":

Here I was going to remove the first "IF"'s for the following reason:

    -There is no need to have an "IF" checking if the param has any value since after that we will have another "IF" checking the value of it, we could just check the value since once it's setted it will be different from "null".

But after thinking a little bit there is a two swords edge in here, because we can take it to make the code shorter, but the fact that there is another "IF" guarding the following code blocks makes the code easier to read and more organized, which in my opinion makes more sense.

If my explanation was a little bit confusing I will leave here an example:

Parent1 {    --> "IF" that I acused to be of no use in the beginning
    child1 {
        //code here
    }
    child2 {
        //code here
    }
}

Parent2 { --> "IF" that I acused to be of no use in the beginning
    child1 {
        //code here
    }
    child2 {
        //code here
    }
}

////

The code has a lot of unecessary conditions, instead of using "elseif (condition)" in some code blocks, there are indeed some codeblocks that need that but for example in line "1321" there is no need for that.

////


Overall Review:

I liked to read this code, has everything needed even tho some things are too much, still is an easy code to understand, in my opinion I would've structured the code a little bit different with more functions specificaly to each section, by doing that, we wouldn't need to create so many "if statements" and we would have a way shorter code, the thing is, once the code is built like that it would have to take a very big refactoring and in my opinion refactorings like that are only needed if, we get into a bug that we can't understand the root of, or we find ourselves in a situation where it's almost impossible to read our own code, or the code hasn't followed basic good software writing practices.

But overall I really enjoyed reading and debugging this code.