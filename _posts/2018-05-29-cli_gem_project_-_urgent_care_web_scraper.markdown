---
layout: post
title:      "CLI Gem Project - Urgent Care Web Scraper"
date:       2018-05-29 12:17:54 -0400
permalink:  cli_gem_project_-_urgent_care_web_scraper
---

		 My first project in Ruby is a CLI application that scrapes the website of a company that provides urgent care. Urgent care is provided to patients that typically cannot wait until the next business day but are not experiencing an illness or injury that is life-threatening. Many urgent care centers are located throughout Massachusetts to treat patients and prevent long wait times in the Emergency Department. My application lists the next available appointment time at urgent care centers in Massachusetts based on location. This provides a quick and easy way to find care.
		 The biggest challenge when coding this project was to find the best way to organize the Scraper class. This class scrapes the website for the desired data and stores it in a separate Office class. All of the relevant data that I wanted was located under the node of ('.et_pb_column_1_4'). However, the relevant data for each office was located in two different ('.et_pb_column_1_4'). This required separating each ('.et_pb_column_1_4') into two separate arrays and then zipping them together in order to form one office_details array where each element contains the relevant data for each office. 

```
def get_clinics;
url_array = [];
digits_array = [];
get_page.css('.et_pb_column_1_4').each_with_index do |location, index|
	if index.odd?
		url_array.push(location)
	else
		digits_array.push(location)
	end;
	url_array;
	digits_array;
end
digits_array[0..16].zip(url_array[0..16]).each_with_index do |office_details, index|
end
  end 
	```
	
	      After getting past this barrier, scraping from each element of the office_details array was simpler. The next challenge was discovering that the Next Available Appointment Time data that I wanted on the second page was contained within an iframe. This required scraping the link for the individual office page, then the iframe link, and then the appointment time data. 
				
			
		doc_d = Nokogiri::HTML(open("https://www.carewellurgentcare.com#{office.url}"));
    doc_i = doc_d.css('.locat').attr('src').text;
    doc_n = Nokogiri::HTML(open(doc_i.to_s));
    office.next_available = doc_n.css('.panel-heading').text.strip.gsub("\r\n", ' ').split(',')[0];
		
		
		
		While challenging, these obstacles taught me the importance of proper planning in order to return exactly the data that you are looking for.
	

