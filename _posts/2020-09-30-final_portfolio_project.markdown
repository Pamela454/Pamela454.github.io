---
layout: post
title:      "Final Portfolio Project"
date:       2020-09-30 22:19:41 -0400
permalink:  final_portfolio_project
---


For my final project I am creating an application that functions as an electronic medical record. For this project, I thought it was important to have two different users so that the application can be experienced as either a patient or as an administrator.  Patients are able to log in and see their account balance. From there they can make a payment towards their balance. As an administrator, you can add a charge to an account. I used the enum attribute in Ruby on Rails to store the value of either a patient or admin in the database. 
```
class Account < ApplicationRecord
	enum status: [:patient, :admin] #keep track of user role 
	has_secure_password #already validates presence 
    validates :name, uniqueness: true
	has_many :departments
	has_many :payments 
	accepts_nested_attributes_for :departments, :payments 
	after_initialize :set_defaults

	def set_defaults
		self.balance ||= 0   #if nil, set default 
	end

 #after_initialize do #default value is patient 
   #if self.new_record?
    # self.status ||= :patient 
  # end
 #end
	
end

```



  Each account can have many payments and many departments associated with it. The departments each carry a charge that totals to the account balance. The payments store the payment information submitted by a patient and update the account balance through a method written on the account model. 
     When the patient logs in they can see their account balance and any department charges associated with the account. They can then choose to submit a payment by credit card. 
		 Redux manages the store and displays the new account balance without refreshing the page. 

