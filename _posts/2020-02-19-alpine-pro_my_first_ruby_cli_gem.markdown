---
layout: post
title:      "**Alpine-Pro /// My First Ruby CLI Gem**"
date:       2020-02-19 01:02:19 -0500
permalink:  alpine-pro_my_first_ruby_cli_gem
---

![](https://cdn.britannica.com/17/83817-050-67C814CD/Mount-Everest.jpghttp://)

Alpine-Pro, my first Ruby project. The purpose of it is to populate a list of potential expeditions the user may be interested in and give a description for the chosen option. Looking back on it, it was only fitting my gem was about mountains. Because this was one heck of a journey! An uphill climb, with many setbacks, doubts and struggles. However, just like reaching the summit of a mountain, I persevered and pushed on. I can honestly say that this one single project has taught me more about being a software engineer than anything else so far. It won't be easy, it'll be very frustrating and confusing at times, but man, is that feeling when you figure out your broken code and finally see your hard work come together worth it.

I began my gem project by creating three classes and cooresponding files. A CLI/Controller class, a Scraper class, and an Expedition class. My next step was to create a basic outline of how I wanted my CLI to look. The purpose of this was for me to be able to just focus on my code and have one less thing to worry about. In addition, there is a sacred rule I live by: "Plan your work and work your plan." After this, I began working on my Scraper class. I wanted to make sure the website I chose was "scrapable". My original website was not, so I had to find a new one. This is why I chose to focus on my scraper first (and it payed off)! Here is my Scraper Class: 

**-----------------------------------------------------------------------------------------------------------------------------------
**
class AlpinePro::Scraper
  
#scraping of expedition names and the url to be initialized with the expedition
  def self.scrape_expeditions 
    index_page = Nokogiri::HTML(open("https://www.adventureconsultants.com/expeditions/"))
    
    array_of_expeditions = index_page.css("div.slide__content")
    array_of_expeditions.each_with_index do |expedition_card|
    name = expedition_card.css("span.slide__title.uppercase").text
    path = expedition_card.css("a").attr("href").value
    AlpinePro::Expedition.new(name, path)
     end 
  end 
 
 #scraping of description from url it was initialized with 
  def self.scrape_description(expedition)
  description_page = Nokogiri::HTML(open("https://www.adventureconsultants.com"+ expedition))
  description_page.search("div#body-content").text.strip  
  end 
  
end 

**-----------------------------------------------------------------------------------------------------------------------------------
**

I first had to scrape to get the expedition names I was looking for from the original url. I also had to scrape a path so that it can be initialized with the expedition name in my Expedition class. This had to be done because the description I wanted to scrape was on a separate page belonging to each individual Expedition.

Here is my Expedition Class where the name and path are initialized:

**-----------------------------------------------------------------------------------------------------------------------------------
**

class AlpinePro::Expedition

  attr_accessor :name, :path, :description 
  
  @@all = []
  
  def initialize(name, path)
    @name = name 
    @path = path 
    save 
  end 
  
  def self.all 
    @@all 
  end 
  
  def save 
    @@all << self 
  end 
  
end 


**-----------------------------------------------------------------------------------------------------------------------------------
**

Once I had these two classes going, it was time to put my CLI together and make everything work together. I created a "start method" to welcome the user and called on some methods to run them in order. In this method, I also called on my scraper, to scrape the expedition names. Then in my next method, the "list_expeditions method", I made sure each individual expedition name was assigned an index (starting at 1) so that it can be interacted with, as the user is technically interacting with the index and not the name. In the next method, "get_expedition" the user is asked for an input to the cooresponding list of expeditions. This method also recognizes if a proper command was input. Finally, there is the "want_description method" which is the "second layer" to the program. It double checks with the user, making sure that they made the correct input. Once confirmed, it prints the description by caling "expedition.description".

Here is the CLI: 

**-----------------------------------------------------------------------------------------------------------------------------------
**

  class AlpinePro::CLI 
  
  #welcome method, calls on scraper to list expedition names
    def start 
      puts ""
      puts "Welcome to Alpine-Pro!"
      puts ""
      puts "Here are expeditions you should check out:"
      puts ""
      AlpinePro::Scraper.scrape_expeditions
      list_expeditions
      get_expedition
    end 
    
  #list method turns the expeditions into a list with index 
    def list_expeditions
      AlpinePro::Expedition.all.each.with_index(1) do |expedition, index|
        puts "#{index}. #{expedition.name}"
      end 
    end 
    
  #get method outputs the expedition list  and receives user input
    def get_expedition
      puts ""
      puts "////////////////////////////////////////////////////////////////"
      puts ""
      puts "Select an Expedition from 1-109"
      input = gets.strip
      index = input.to_i - 1 
      if index.between?(0,108)
        expedition = AlpinePro::Expedition.all[index]
      puts ""
      puts "///  You Chose: #{expedition.name}  ///"
      want_description(expedition)
      elsif input == "exit"
      else 
        puts "Sorry I didn't understand that command"
        get_expedition
      end 
    end 
    
    #description method receives the descriptions from the scraper class
    def want_description(expedition)
      
      expedition.description = AlpinePro::Scraper.scrape_description(expedition.path)
      puts ""
      puts "Do You Want To Continue (Y/N)"
      input = gets.strip.upcase
      until ["Y","N","YES","NO"].include?(input)
        puts "Please Type Y or N"
        input = gets.strip.upcase
      end 
      if input == "Y"
        puts ""
        puts "/////////  Your Next Adventure: #{expedition.name}  /////////"
        puts ""
        puts expedition.description
      else 
        puts "you ended"
      end 
    end 
      
   
end 

**-----------------------------------------------------------------------------------------------------------------------------------
**

All in all, this first project was one of the most rewarding experiences in my life. (And I have had many). As tough as some parts were (scraping), I acquired many traits that will, with hard work, round me into the full-stack software engineer I dream of becoming. Persistance, Attention to detail, and a love for creating something from scratch.



