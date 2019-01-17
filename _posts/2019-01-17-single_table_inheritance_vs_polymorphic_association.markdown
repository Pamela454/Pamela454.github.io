---
layout: post
title:      "Single Table Inheritance vs. Polymorphic Association"
date:       2019-01-17 23:50:42 +0000
permalink:  single_table_inheritance_vs_polymorphic_association
---


For my Ruby on Rails project, I needed to choose a setup so that two different users could access the application. I chose a single table inheritance because my two users shared most of the same data. The table would also be small and not accessed by other tables. Searching becomes more time consuming when the table is large and has many nil values. 

One user acts as a patient and is able to send messages to physician users. Their profile is simple and consists of a name, email address and password. The other user is a physician and has the same data as a patient as well as an NPI number that is unique to each physician as well as their specialty.  

The application allows patients to submit medical questions for physicians to answer. The single table inheritance design setup allows for all users to inherit from the user class reducing and streamlining the code. 

