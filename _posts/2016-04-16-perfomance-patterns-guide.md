---
layout: post
title: Performance debugging patterns and guide
comments: true
---

Working on 5 different kinds of project on performance improvement analysis, you get to know the pattern in performance debugging.

I have worked on analysing performance problems in projects that are developed in different languages and for different purpose. 
Still, I can find a pattern in performance problems.

If you are starting on debugging a performance issue then this post will help you narrow down the problem you face in the project. 

Before that you need to understand few terminologies,
  
<h3>Performance vs scalability</h3>
   
   In the book Pro-JavaEE by Steve Haines, discusses the topic of scalability and performance. 
   Here's Steve's definition of Scalability vs Performance:
   
  <i> "The terms “performance” and “scalability” are commonly used interchangeably, 
  but the two are distinct: performance measures the speed with which a single request can be executed, 
  while scalability measures the ability of a request to maintain its performance under increasing load. 
  For example, the performance of a request may be reported as generating a valid response within three seconds, 
  but the scalability of the request measures the request’s ability to maintain that three-second response time as the user load increases."</i>
  
  Scalability is a whole new problem. Let us not touch that for now, These are some of the examples of performance problems which I faced personally,
  
   1. REST API which responded in 500ms when there is no user. The same API responded in 40 Sec or not even responded when 50 concurrent users accessed it.
   2. A script which can read and process a single file with 10 lines in less than a second, whereas takes hours of processing for 50+ files 
      with 1000 lines.
   3. A web application which loaded pages in seconds, never loaded for 100 concurrent hits.
   
   The above problem will continue even when you increase the servers capacity (CPU, Memory and even new servers).
  
<h2> Performance Pattern </h2>

Now with understanding of the term performance, we will see the list of performance pattern.

<h3>Data is the problem</h3>

The biggest bottle neck in performance in almost all projects in on how you handle the data.
It doesn't matter whether you use a database management system like MySql, Oracle or Object based database like LDAP or even flat files, that's the palce you have to check first.
I will cover on how to identify and correct the bottleneck in data access for every data source as a separate post.

<h3> Latency on dependent systems </h3>

Next checkpoint is when you use a 3rd party service. If you are dependent on external system then you have to check the behaviour here. 
Any external calls using REST, SOAP should be added to watch. You can easily find this by adding log statements before and after the calls.

<h3> Is there a Cache ? </h3>

Most complex system has a cache. You cache heavy processed data, yet there is a performance problem. Then you have to look for cache hits and miss ratio.
If you have more miss, then you have to re-look on the way in which you cache the data.May be you can increase the cache expiry.


Next post will cover on steps to narrow down the exact problem.

Goodluck and Happy debugging.

