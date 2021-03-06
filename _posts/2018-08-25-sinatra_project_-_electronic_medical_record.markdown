---
layout: post
title:      "Sinatra Project - Electronic Medical Record"
date:       2018-08-25 23:13:31 -0400
permalink:  sinatra_project_-_electronic_medical_record
---


For my Sinatra project, I developed an application that would function as an electronic medical record.  Medical records provide clear, easy access to patient data. This allows clinicians to have up to date access in order to make clinical decisions. 

This application allows patients to log in to view their medical history and active medical problems that their physician is working on. Physicians are able to add patients to care and add and edit their medical history and problems. 

Validating the data entered into the database and ensuring that only physicians have editing access were big challenges for this project. 


```
  validates :username, :presence => true, :uniqueness => true
  validates :npi, :presence => true, :uniqueness => true, length: { minimum: 10 }
  validates :password, :presence => true, length: { minimum: 5 }
	
```


The above code was entered into the physician model. This way every new physician entry must have a unique username, password, and an NPI number. The NPI number is a unique number that physicians have for their work. 

I included a helper method that will tell whether a user is currently logged in:

```
helpers do
		def logged_in?
			session[:id] != nil
		end
  end

```


This method checks whether it a user is logged in for pages only to be viewed by users. Pages to allow editing and creating patients are only accessible due to code that checks is the current session id is equal to the physician id. This protects the integrity of the data and improves the user experience by only showing the user links and fields that are relevant to them. 
