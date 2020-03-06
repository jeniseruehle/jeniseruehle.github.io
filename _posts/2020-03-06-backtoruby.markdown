---
layout: post
title:      "BackToRuby"
date:       2020-03-06 16:58:02 -0500
permalink:  backtoruby
---


Hello! It's been a while I know...

Between holidays, transitioning to a new role at work (a less stressful environment which is a good thing!), and trying to stay on top of course work I've been a little behind on my blogging.

I'm currently working my way through Mod 6: Object-Oriented Ruby and slowly working my way towards my first project. Transitioning back to Ruby after a brief work through HTML was not as hard as I expected but definitely made clear what portions of Ruby I have not quite understood completely yet like iteration! I also learned that probably like most I really enjoy Object Oriented over Procedural.

Luckily, I'm getting plenty of practice with Section 11's Labs. Specifically, working through Email Parser. These were both simple enough to build and allowed me to work more with methods like **.split** and **.collect**.

After running my tests and checking out the specs on the Email Parser Lab, I created an **EmailAddressParser** class and initialized it with a string of unformatted emails to be separated (or parsed) into an array of unique email addresses using an instance method **parse**.

To start, I created an attribute accessor **csv_emails** within the EmailAddressParser class and initialized my class with the **csv_emails** instance variable. Next, I defined my parse method. To define my method I decided the easiest way to parse my emails was to iterate over the unformatted emails and **.split** them from their unformatted state and then **.collect** each one into a new format seperated by a comma (',').  

Once that was done, I needed to put my newly formatted emails into an array and to be sure that only unique addresses were saved and not any duplicates. While flipping through my notes I remembered from a previous lesson in Mod 5 on Iterating over Nested Hashes using the **.flatten** method to return a one-dimensional array and then using the **.uniq** method to remove any duplicates from an array. At first, I thought I could add both methods to the end of email.split(',') quickly realizing this broke my code - putting **.flatten.uniq** *after* ending my iteration was what made it click.

*Here's the actual code:*

class EmailAddressParser
  attr_accessor :csv_emails
  
  def initialize(csv_emails)
    @csv_emails = csv_emails
  end
  
  def parse
    csv_emails.split.collect do |email|
      email.split(',')
  end 
    .flatten.uniq
  end   
end 



