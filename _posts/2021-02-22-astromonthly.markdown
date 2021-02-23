---
layout: post
title:      "Astromonthly"
date:       2021-02-22 18:02:47 -0500
permalink:  astromonthly
---


Whew! This project has been the hardest one yet but also the most rewarding. I actually love my app idea and plan to continue building on it and designing it after review is over.

**Astromonthly** is a web app that provides monthly horoscopes and the option for you to journal and track your monthly themes. I chose this project because I guess I would say I am both an amateur astronomer and astrologer. Astronomy is actually what led me to astrology. I know it's not for everyone but anyone that wants to learn more than just their mainstream Sun sign, astrology is a fun and ever-evolving practice to learn about. 

At first, I just wanted make a horoscopes app but the more I sketched it out, I decided I wanted a way to tie in some functionality that users could interact with like journaling. Journaling is an excellent way to express your thoughts/feelings and one of my favorite things about journaling is the ability to look back at past journals to see both your progress and overarching themes in your life. Journaling works well with astrology because there are always events to work with. I made the decision to start with simple monthly horoscopes - which follow the path of the sun throughout astrological houses each month (these fancy astrology terms start to make sense once you look at your chart). I eventually will add a section with astro-basics and potentially more horoscopes/journal prompts like full/new moons and Mercury retrogrades.

This project was just as fun as it was frustrating and I can say picking something I am passionate about is what kept fueling me to get through and make it just right (no matter how many hours spent on working out the bugs).

I have to say I spent the most time trying to get my Omniauth to work. I didn't want to use the Devise gem because I knew it was possible to do it without (I also never used Devise before and didn't know what it would do to the other functioning parts of my app; I had come too far and coded too much to try it out lol). I started with trying to integrate the Google OAuth because I didn't have a Facebook Account. After a few days of extensive Google searches, combing through Stack Overflow, and multiple recodes... I decided to give up on Google and try a tutorial on integrating the GitHub OAuth. Well.. GitHub was also a failure - the errors I was running into were the same ones I was having with Google OAuth. It seems that several other people have also had similar issues with the newest version of the OAuth gem. I finally caved and signed up for a Facebook account because it seems Facebook OAuth was the one that had been the most successful for others. 

Listen, it honestly felt like I hit the lottery when the Facebook OAuth finally went through! I spent over a week just trying to get any OAuth to work - I quickly committed and pushed my code to GitHub, for fear of losing it and a slight worry that it was just a fluke!

For anyone else who may be struggling with this, I did a number of things to get it to work and I'm honestly not quite sure if all of it is needed but here is what I did.

I added these gems to my **Gemfile** which helped with a couple of early errors I was getting:

```
gem 'omniauth'
gem 'omniauth-facebook'
gem 'omniauth-rails_csrf_protection'
gem 'dotenv-rails'
gem 'thin'
```

Then after following along with the OmniAuth lesson tutorial on getting everything setup on the Facebook side, I came back and set up my **config/initializers/omniauth.rb** file:

```
Rails.application.config.middleware.use OmniAuth::Builder do
    provider :facebook, ENV['FACEBOOK_KEY'], ENV['FACEBOOK_SECRET']
end
```

Next, I set up my **.env** file in the root of my app and added my FACEBOOK_KEY and FACEBOOK_SECRET to it. After this, I went to my **.gitignore** file and added `.env` to it, to be sure I didn't accidentally share my access keys.

Then it was time to get to work on my **Sessions Controller**, to actually get my logic together. At first, I tried running two separate `create` methods (one for normal users logging in and one just for facebook users) because stress and fear had me worried I'd break my original `create` method which was working just fine BUT luckily after getting it to work separately, I was able to combine them without issue:

```
    def create
        if auth
            @user = User.find_or_create_by(:email => auth["info"]["email"]) do |u|
               u.name = auth["info"]["name"]
               u.password = SecureRandom.hex
            end
            session[:user_id] = @user.id
            redirect_to user_path(@user)
        else 
            user = User.find_by(email: params[:email])
            if user && user.authenticate(params[:password]) 
                session[:user_id] = user.id
                redirect_to user_path(user)
            else
                flash[:error] = "Uh oh! Login info incorrect, please try again."
                redirect_to login_path
            end
        end
    end
```

And don't forget to put the `auth` method in the `private` section:

```
    def auth
        request.env['omniauth.auth']
    end
```

Next, I made sure the correct paths were set up in **config/routes.rb**, so I could actually access the controller logic (this a bit I found on stack overflow and it was pretty essential for me to get my links to both `get` AND `post` -- before this, I kept getting **Routing Error:: No route matches [GET] "auth/facebook"** on my login links - I'll get to this next):

```
match '/auth/:provider/callback' => 'sessions#create', via: [:get, :post]
```

Almost there! After my route was set up, it was time to see if it all actually worked by putting a link in my views. My link is on the Login page under my Session view and I set it up like:

```
<%= link_to "Log in with Facebook!", '/auth/facebook', method: :post %>
```

And finally it's done! I was able to successfully log in with my brand new Facebook Account and start using my web app.
Very exciting stuff.

Because I spent SO much time building this out, I did very minimal design work but I'm actually kind of happy about that since Frontend is up next and I can truly learn how to make it beautiful without the looming feeling that I'm falling behind! I'm super excited about Frontend because I am definitely someone who LOVES design.

Anyway, hope this helped you in some way! Goodluck on your journey and Happy Coding!


