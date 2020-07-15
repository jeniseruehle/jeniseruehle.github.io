---
layout: post
title:      "TarotToGo CLI "
date:       2020-07-04 12:51:38 -0400
permalink:  tarottogo_cli
---


I cannot believe it took me so long to complete my CLI. To be honest, I have dreaded my first project almost from Day 1, I really *really* psyched myself out about it - I deeply believed there was no way *I* could write a program on my own and have it actually work. But time and excuses aside, today I finally figured out one of the last hangups in my code and I have completed and really love my CLI. 

For my project, I wanted to create a program that would scrape a website and provide the user with quick meanings for all 78 Major and Minor Arcana Tarot Cards.

![](https://i.pinimg.com/originals/c4/a5/4d/c4a54dd762ed4bdf2a5c5fba0b338b53.gif)

Completing my flow chart and the initial checklist gave me a small boost in confidence and enough excitement to push through the anxiety of really getting started. I began with watching the videos, reviewing the Student Scraper Lab, and finally setting up my environment. And after initial set up, I was quickly met with internal resistance and fear. 

One of my early setbacks was the first website I chose to scrape from. After much frustration, not being able to scrape things correctly, and the cards being in the wrong order, I decided to scrap my first Github repository all together and start over again. This time with a better website, BiddyTarot.com - her code was clean, all of the cards were in the correct order, and each had quick easy descriptions that were perfect for what I wanted to accomplish with my CLI. 

My program begins with welcoming the user and giving them a numbered menu of the five cardsets to choose from: Major Arcana or one of the four suits: Wands, Cups, Swords, Pentacles. Once a cardset is chosen the second menu displays all the cards that are in each set. The user is then presented with the choice for which card they would like to see the meaning of. Next, the user types in the name of the card they would like to see and once they hit enter the Upright and Reversed meanings are displayed along with a choice to return to the original menu to choose another card or to exit the program. 

Pretty simple right? Well, coding the cardset menu and getting it to run was a piece of cake. It lulled me into a false sense of hope that the rest of the coding would be just as breezy...

![](https://media2.giphy.com/media/pWIak75z5nNWU/200.gif)

Then came the actual scraping of information... at first I couldn't decide how and what exactly I wanted to scrape and after many failed attempts, I almost decided to ONLY scrape the 22 Major Arcana cards. I spent several hours for a few days not returning much of anything and then the despair set in followed by the doubt and procrastination monsters. I gave myself all kinds of excuses - I had to work, I had housework, I had banana bread to bake... all the while knowing there was no way I could escape this project and I certainly couldn't give up.

I finally had a moment where I could not avoid it any longer, I had to buckle down and just work my way through it. I rewatched the videos, went back over all my notes in detail, and reviewed the Music CLI, Student Scraper and Kickstarter labs. When I really got into it, it took me almost a full day to get my scrape to work but it DID work and I was in awe. From that moment on, it was all a matter of figuring out how to get everything else to work properly.

My biggest issue was once I got the information to scrape and display properly, three of my cardsets kept returning a '404 Not Found (OpenURI::HTTPError)'...

![](https://media.tenor.com/images/2a5b6d4e3a802aa4285e2584a5c4b48a/tenor.gif)

Turns out some of the cardsets had only half of the link in their code and the other cardsets had the full link listed. My first thought was %$@#! and my next was Google. I came across a Stack Overflow thread where someone had a similar problem and mentioned writing an if/else statement (to which I then felt like "DUH I knew that"), the first attempt:
```
    index.css("div#biddy_card_list").each do |cards|
      cards.css(".card_item a").each do |single| 
        if single.include?("https://www.biddytarot.com/tarot-card-meanings/") 
          card_link = "#{single.attr('href')}"
        else
          card_link = "https://www.biddytarot.com/#{single.attr('href')}"
        end   
```

Except, it STILL didn't work. I tried all different combinations of the link text, I thought of switching to a case statement, I tried an ".exclude?()" method I saw mentioned - all to no avail. So, I took a day and decided to come back to it later. Today I came across a "Nokogiri in Rails" thread in my search, that mentioned adding an ['href'] and shortening the link text to just ("https"):
```
    index.css("div#biddy_card_list").each do |cards|
      cards.css(".card_item a").each do |single| 
        if single['href'].include?("https")
          card_link = "#{single.attr('href')}"
        elsif
          card_link = "https://www.biddytarot.com/#{single.attr('href')}"
        end 
```
AND IT WORKED!!! All my cardsets are now scrapable and you can see every Upright and Reversed meaning for all 78 Tarot Cards.

![](https://i.pinimg.com/originals/db/c6/59/dbc6597b27b388e63bb782875fc7140c.gif)

So not only am I embarrassed for thinking I couldn't do this but I realized that errors are your friends, making the mistakes can lead to the answers and really using my research skills are crucial to being a developer. And though it might sound cheesy, I am pumped to complete this and I am so excited to continue learning to code!
