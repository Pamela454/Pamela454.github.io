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
     When the patient logs in they can see their account balance and any department charges associated with the account. They can then choose to submit a payment by credit card through the payment form. Submitting a payment through the payment form dispatches an action to add a payment as well as get the current account so that the account data refreshes on the user page. Redux manages the store and displays the new account balance without refreshing the page. 
		 
		 Add Payment Action
		 
>  export const newPayment = (paymentData, history) => {
>  
>   return (dispatch) => {
>     const url = `http://localhost:3001/api/v1/accounts/${paymentData.account_id}/payments/new`;
>     
>     return fetch(url, {
>       method: "POST",
>       credentials: "same-origin",
>       headers: {
>         "Content-Type": "application/json",
>       },
>       body: JSON.stringify(paymentData),
>     })
>     
>       .then((res) => res.json())
>       .then((payment) => {
>         console.log(payment);
>         if (payment.error) {
>           alert("error");
>         } 
>         else 
>         {
>           dispatch(addPayment(payment.data));
>           console.log(payment.data);
>           //call additional action to update account
>           dispatch(getAccount(payment.data, history));
>           //history.push(`/accounts/${paymentData.account_id}`);
>         }
>       })
>       .catch(console.log);
>   };
> }; 

Account Component Displaying User Data 

> import { connect } from "react-redux";
> import React from "react";
> import Accounts from "./Accounts.js";
> import { withRouter } from "react-router-dom";
> import { Button } from "react-bootstrap";
> import { getDepartments } from ".././actions/currentDepartments.js";
> 
> 
> 
> const Account = (props) => {
> 
>     const handleClick = (e) => {
>         e.persist();
>         e.preventDefault();
>         props.getDepartments(props.account.account.id, props.history);
>     };
> 
>     return (
>         <div className="container">
>             <div className="row align-items-center">
>                 <div className="col">
>                     <h2>
>                         {" "}
>                         {/* can assign a key by converting to an integer? item index? */}
>                         <label> Account Name </label>
>                         {props.account
>                             ? ` - ` + props.account.account.attributes.name
>                             : null}
>                         <br></br>
>                         <label> Account Balance </label>
>                         {props.account.account.attributes.balance != null
>                             ? `  $` + props.account.account.attributes.balance
>                             : null}
>                     </h2>
>                     {props.account.account.attributes.status === "patient" ? (
>                         <Button onClick={handleClick}>View Charges</Button>
>                     ) : null}
>                     {localStorage.getItem("status") === "admin" ? (
>                         <Accounts {...props} accounts={props.accounts} />
>                     ) : null}
>                 </div>
>             </div>
>         </div>
>     );
> };
> export default withRouter(connect(null, { getDepartments })(Account));
> 

On the backend several methods on the payment model update the user's account balance and the balance of the department. This new data is then displayed on the patient account front end as soon as the url changes to the user's account. 




