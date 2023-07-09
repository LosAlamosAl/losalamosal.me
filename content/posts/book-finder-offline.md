---
title: "Book Finder: Locating Misplaced Cookbooks"
subtitle: "A joint project with my son to learn AWS Serverless"
date: 2023-07-05
type: post
draft: true
tags: ["aws", "lambda", "dynamodb", "cloudformation", "serverless", api gateway]
---

I own almost 400 cookbooks. Acquired over many years, each always lived in the same spot in my bookshelves. This consistency allowed me to develop a spatial memory&mdash;when looking for a specific cookbook I could immediately find it on the shelf. That all changed when my wife and I upgraded our bookshelves and relocated the whole collection to another room. We tried to move them systematically, and retain some kind of spatial locality, but that all fell apart during the process of moving the books. I could no longer rely on my spatial memory when looking for a book&mdash;I had to scan all the shelves hoping to see the book. This annoyed me so much I decided to write an application to find the books for me.

<!--more-->

At about the same time my son, [Marlon](https://mcpherson.dev) (more on him later), decided to take some time to learn additional technical skills and take is carreer in software development to the next level. Since I had already selected AWS Servelress to prepare for **The Killer App**&trade;, we decided to design a "Book Finder" application and code it with AWS Serverless technologies. We would design it together but he would write the front end while I focussed on the back end processing. We took a few AWS classes and worked up a design. This post describes my part&mdash;the offline processing that prepares the input data for his part (the user's interaction with that data). I'll briefly describe his front end work at the end of this post.