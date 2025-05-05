---
layout: post
title:  "Music streaming converter"
date:   2025-05-05 13:14:13 -0500
categories: jekyll update
---
PROBLEM!!!!!!!!!!!!!

I’ve been with Apple Music for the last few years and had around 1,300 songs in my library. All my friends use Spotify, and I always feel left out when they start a Spotify Jam. I recently found out that you don’t need a paid Spotify account to join a Jam—but that’s beside the point. Being left out sucks, so I decided it was finally time to get a Spotify account and leave Apple Music for good.That’s when I began the journey of converting all my songs from Apple Music to Spotify.At first, I tried doing it by hand. But after the fifth song, I realized it wasn’t sustainable. It took about 10 seconds to find and like a song on Spotify, which meant:

10 * 1300 = 13,000 seconds
= 216.6 minutes
= just over 3.5 hours
So, like the smart engineer I am, I spent 10 hours automating the process. 😅 

Problem 1: Getting Music from Apple
Did you know there’s an Apple Music API? Did you know it costs $100 to use it? When I found that out, I nearly gave up. But then I remembered—we’re engineers. Money can’t stop us.
Enter Puppeteer (sorry, Apple). It’s a JavaScript library used for web scraping. All I really needed were the song names and artist names, so I used Puppeteer to log into Apple Music through the browser and start scraping.At first, I was only getting the same 10 songs over and over again. Turns out, the HTML only holds info for what’s currently visible on the page. So, I improvised. I had the script scroll slowly, scrape the songs, scroll some more, and repeat. With this approach, I eventually got all the songs—though with some duplicates—in a CSV file. 

Problem 2: Deleting Duplicates
To clean up the CSV, I used Go. I parsed the data and removed any duplicates or noise. Now I had a clean list, ready to be sent to the Spotify API.

Problem 3: Spotify API
I didn’t want to use any third-party libraries here—I wanted to learn more about how REST APIs work.
The first challenge was converting song names and artists into Spotify track IDs. This is how Spotify identifies songs and how I’d add them to a playlist. I made an API call that looped through the CSV and fetched all the track IDs, saving them to a new CSV. From there, I created a playlist and added all the tracks using a POST request. Spotify allows up to 100 tracks per request, so I batched them and sent them in chunks.

I want to explore more with this project. Next steps:Try going from Spotify to YouTube and back again.Build a UI with user credentials so anyone can use it to switch platforms seamlessly.If all goes well, I might pay for the Apple API and make this a real mini-product.

I’m thinking:
Backend: Go
Frontend: Next.js
Database: PocketBase
We’ll see what the future holds.

Cheers for now,
Dylan McCarthy




