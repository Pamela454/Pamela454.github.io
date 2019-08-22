---
layout: post
title:      "Hoisting and Scope for Beginners "
date:       2019-08-16 17:13:27 -0400
permalink:  hoisting_and_scope_for_beginners
---

There are two concepts that are important to be familiar with when first learning to code in Javascript. Misinterpreting them can cause you some frustration when searching for errors in your code. 
										 
Scope are the variables and functions available for use within the current execution context. The execution context is the environment in which the code is being run.  In Javascript the scope could be the global scope, the function scope, or the block scope.  Variables declared in the global scope are accessible anywhere throughout the code. Within an execution context, when a variable is referenced, that context can look further up the scope chain to find the declaration of the variable. So a function within a function can search both the outer function and the global scope. Keep this in mind when trying to access values stored in variables. A reference error may indicate that the variable was declared and assigned, just not accessible within your current scope. 

```
        //Global variable accessed from within a function
				
        let userId = function retrieveuserId(){

              return $('h2#userid').data('user-id')

            }  

 function listenForClick() {

	     console.log('setting up click handler');

	$("button#messages-data").on('click', event => {

	    console.log('button clicked');

		  event.preventDefault()  


		var url = `${userId()}/messages.json`

		fetch(url,   {

        	})

			.then(res => res.json()) 

			.then(allMessages => {

				$('.square').html('')

				console.log(allMessages)



				allMessages.forEach(message => {

                    let newMessage = new Message(message)

                    let messageHtml = newMessage.postHTML()

                    $('.square').append(messageHtml)

                })

			})

			.catch(error => console.error('Error:', error));



	})

}

```
										 
Hoisting is when a variable or function declaration is available at the top of it's scope even though the declaration is below the call to the function or variable. When a function is invoked prior to its assignment, the function is still executed due to hoisting. Function declarations are hoisted before variables are. Using var to declare  a variable after the variable is invoked, will return "undefined". Using let and const and then referencing them before they have been declared will return a reference error instead of undefined.  

``` 
     //returns the desired text 'Patient Message' due to hoisting 

       messageRetriever();

               function messsageRetriever() {
                      return ’Patient Message’;
                  }
```
										 
The addition of let and const in ES6 can cause some confusion around the concepts of scope and hoisting.  Prior to ES6, most variables were declared with var. With var you can declare a variable twice in the code without receiving an error message. Const and let will not allow you to declare a variable (give it a name) a second time. Const also cannot be reassigned (set to a value). When a variable is declared without a keyword (such as var, let or const), it is automatically considered a global variable and is accessible within the global scope no matter where it was declared in the code.  When var is declared in a block, it can still be accessed outside of that block scope. Const and let are block scoped and when declared in a block, will not allow the values to be accessed outside of the block and will return an error. 
										
