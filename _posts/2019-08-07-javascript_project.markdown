---
layout: post
title:      "Javascript Project"
date:       2019-08-07 13:45:08 -0400
permalink:  javascript_project
---

              
               
For my Rails project, I created an application that would allow users who registered as patients to ask medical questions to physicians. Users who register as physicians can answer these questions. 
							 
For my Javascript Project, I used this language to add the ability for my patient users to see an index of all of the questions that they have asked as well as a show page which displays all of the details of that question as well as all of the responses that this question has received. This allows the user to quickly find information that is relevant to them and quickly flip back and forth between questions as they do not have to leave their own personal user show page. To implement the display of the responses from physician users, I needed to display both the question that the user asked as well as all of the physician responses from the response objects. The responseHandler function sends questions asked by a particular user in the form of JSON data. This data is used to create Javascript objects that are passed on to a prototype function which will display formatted HTML data. 

```
Message.prototype.formatShow = function () {

	var responseHtml = "" 
	this.responses.forEach(function(response) {
			var newResponse = new Response(response)
			 responseHtml += newResponse.response
	}) 

	let postHtml = 
	`  <h3>Id:${this.id}</h3>
	   <h3>Title: ${this.title}</h3>
	   <h3>Question: ${this.question}</h3>
	   <h3>Response: ${responseHtml}</h3> 
	`
	return postHtml
}
```

Within the prototype function, I wanted to add HTML that displayed the responses to each question. I iterated over each message object and accessed the responses using dot notation. From this new response objects were created and stored in a variable. The response property is accessed on the Response object and stored in a variable. This variable is displayed in a template literal as HTML with the message properties. 
							 
The user can also ask a new question in order to receive help from the online physicians. To do this, they are directed to a new question form which when submitted displays all of the information submitted as a new question. This confirms to the user that their questions was submitted and lets them review all of the information that they physician will see again without leaving the page. These features enhance the user experience by displaying results more quickly and reducing the number of clicks that the user has to perform. 


