# Scope and execution context exercise
  
## Directions

Discuss the following questions amongst your group. Take a few minutes to work through each referencing the lesson and the linked resources at the bottom of the notes for pointers. Ensure that every group member gets a chance to talk through at least one question and discuss your conclusions as a group.

1. How many execution contexts are contained within this block of code? In what order are they executed (try sketching out the "execution stack"):

    ```js
    function a () {
      function b() {
        c(); 
        console.log("1 - What is my execution context?")
      }  
      b();
      console.log("2 - What is my purpose?");
    }

    function c() {
      console.log("3 - Where am I?"); 
    }

    a();
    ```

2. Determine the individual scopes which exist within the following code. Will each `console.log()` print the expected value, or if not, why?

    ```js
    const lovesWaffles = 'LeslieKnope';

    function citizensOfPawnee() {
      console.log(lovesWaffles);
      const lovesBaconAndEggs = "Ron Swanson";
      
      function yaHeardwithPerd() {
        console.log(lovesBaconAndEggs); 
        const lovesShoePolish = "Andy Dwyer";
        mouseRat(); 
      } 

      yaHeardwithPerd();
    }

    function mouseRat() {
      console.log(lovesShoePolish); 
    }

    citizensOfPawnee();
    ```

3. What is `this` referencing in each respective instance below? Based on each output, is the value of `this` dependent on scope or execution context? 

    ```js
    function whatIsThis() {
      console.log("This is:", this); 
    }
    whatIsThis();

    const thisOrThat = {
      methodOne: function() {
        console.log("methodOne:", this); 
        function methodTwo() {
          console.log("methodTwo:",this); 
        }
        methodTwo();
      }
    }
    thisOrThat.methodOne();

    const notThisAgain = {
      bananas: 'in Pyjamas'
    }
    notThisAgain.withANewMethod = whatIsThis;
    notThisAgain.withANewMethod();
    ```
