---
id: 435
title: Sing a song of software, bubbles full of lies; 4 and 20 years of stocks audio-lised with Py
date: 2011-10-10T11:44:08+00:00
author: Samuel Spencer
layout: post
guid: http://www.kidstrythisathome.com/?p=435
permalink: /2011/10/sing-a-song-of-software-bubbles-full-of-lies-4-and-20-years-of-stocks-audio-lised-with-py/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Data
  - Drivel
  - Programming
tags:
  - Apple
  - Google
  - Microsoft
  - music
  - programming
  - stock
---
## <span class="Apple-style-span" style="font-size: 13px; font-weight: normal;">I&#8217;ve been recently toying with the idea of using music as a format of exploratory data analysis. While the use of <a title="Slashdot - Network-Monitoring Data Put to Music" href="http://it.slashdot.org/story/06/02/09/1325225/network-monitoring-data-put-to-music">sound to monitor data isn&#8217;t new</a>, its still relatively uncommon. As I occasionally find myself trying to make sense of large data sets finding a way to quickly analyse them, to find the points of interest can be quite tedious. So I thought about ways someone with no music skill could generate sound from data, and produce something relatively melodic, and useful for highlighting patterns and anomalies in the data.</span>

<span class="Apple-style-span" style="font-size: 20px; font-weight: bold;">Sing a song of software,</span>

To test this out I put together a little tune, that covers the past 24 years of stock information from Microsoft (Piano), Apple(Clarinet) and Google(Xylophone). The pitch is proportional to the price of the stock with low tones being low prices and high be high. While the volume of each instrument is proportional to the volume of sales over the period, so when you hear a quiet sound that is a low volume day, while loud note is a period of higher trading volume.

There are two versions of the music available:

A shorter 2 minute, up-tempo version using weekly stock prices: [OGG](http://bit.ly/qPpKZv "Google Docs - SASOS Short OGG"), [Midi](http://bit.ly/r8XkSN "Google Docs - SASOS Short OGG") &#8211; This one is short and to the point, but some of the nuances, like big daily trade spikes are missed.

A longer, 17 minute, version using daily prices: [OGG](http://bit.ly/pZScem "Google Docs - SASOS Long OGG"), [Midi](http://bit.ly/odhw3q "Google Docs - SASOS Long Midi") &#8211; This one is a little monotonous at the start, but you can hear Apple come from a tiny instrument in the background to a larger force much better. It also lets you hear some off Apples big trading days.

## Bubbles full of lies;

A few things to listen out for:

  * Early on, listen for Microsoft&#8217;s speedy accent during the 2000&#8217;s tech boom, and an even quicker decline. (About 1:00 in on the quicker version)
  * Apple, has for a long time a consistently low trade volume, however occasionally you will hear loud piano strikes starting from the early 2000&#8217;s. (About x minutes in.) These are peaks of stock sale, probably around MacWorld and iPod/Phone/Pad announcements.
  * After about 2005, you can hear Apple and Google slowly rise in volume and stock price, while Microsoft remains in a consistent range throughout the same period. (After 2:00 in the short version)

## 4 and 20 years of stocks,

The data that all of this was pulled from was the historical stock prices data sets available on [Google Finance](http://finance.google.com "Google Finance"). Why 24 years worth &#8211; because it fit with the theme of the nursery rhyme I was trying to mimic. Its pretty touch and go as to what data you can download from Google Finance, but to be fair, from my understanding this is an issue with the exchanges rather than with Google.

## Audio-lised with Py(thon).

So the nitty gritty on how it works:

Its a python script that loops through a set of files of output data from Google Finance and using [midiutil](http://code.google.com/p/midiutil/ "Google Code - MidiUtil") creates a Midi file. Each day (or weeks) datapoint is weighted so the values remain within a specific range for a specific instrument and the volumes are adjusted so that each instrument can be detected. Without either of these it really is quite a mish-mash of sound.

This output Midi file is then run through Timidity++ to create an Ogg/Vorbis file. Converting to Ogg is only necessary for consistency, but both the Midi and the Ogg are available.

## Future work and ideas

Well the goal is to be able to use a technique like this to listen to large multi-variate datasets, that have either a time dimension, or a continuous dependent variable (heights, weights, etc&#8230;). As long as one dimension has values that are relatively evenly and closely distributed with few overlaps and a wide enough spread it should be possible to &#8216;graph&#8217; probably any dataset meaningfully as audio.