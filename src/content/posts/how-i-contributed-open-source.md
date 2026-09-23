---
title: My First Open-Source Contribution; A QLever Story
author: Mete Gonultas
pubDatetime: 2026-09-23T03:06:31Z
slug: first-open-source-contribution
featured: true
draft: false
tags:
  - SPARQL
  - QLever
  - Database
  - SQL
description:
  My first ever open-source contribution and everything that went wrong. A story
  full of failures and go-to-definitions.
  
---

> How Many Times Can One PR Fail Before It Merges? (Asking for a Friend)

<figure>
  <img
    src="/images/qlever.png"
    alt="Brief of the QLever repo by University of Freiburg"
  />
</figure>

## How did I meet with QLever

I am MSc of Computer Science student at University of Freiburg (shout to beatiful city Freiburg). Currently I'm at the beginning of the third semester by the time of writing this blog. When I was in my first semester, I took the Databases and Informations System course which we were seeing the fundamentals of databases with a little bit of web development flavor. Honestly, I was enjoying the databases course contrary to the databases course I took undergrad.

### But why did I enjoy the databases course here so much? 

Well, I believe the databases course in Uni Freiburg is the perfect balance between practice and theory. You see query planning basic, joins, ranking and evaluation and many more things but you also get to implement the algorithms covered in the class. 

Another factor in why I love this course is the instructor. Prof. Hannah Bast is the head of the chair of Algorithms and Data structures. And I must say Prof. Bast is enthusiast at what she does and make the class so much fun, especially compared to the course I took in undergrad. 

Fortunately, the video lectures of Databases and Information Systems course is publicly available and you can reach it via [here](https://ad-wiki.informatik.uni-freiburg.de/teaching/DatabasesInfoSysWS2526) and can get benefit. How awesome is that?

### Lets get back to my journey.

Towards to end of the first semester, I thought that I might give a try emailing to TA since I was having little to none interest in AI courses at that time. I know it sounds a bit off since everything, literally everything, in cs right now somehow related to AI, but I guess I wanted to try new things since I tried AI, ML, DL when undergrad. Then I had mailed about my interest in the course to Robin who will be mentoring me whole semester. Robin explained everything regarding how one could participate in the Databases lab and offered me a couple of roadmaps. I can choose either:
* taking a study project and can start shaping my future-thesis in databases lab or
* taking a lab here and can work on QLever which is home-powered sparql engine of Uni Freiburg.

At that time, I was not sure about whether I would REALLY enjoy working at Databases Lab as much as I enjoyed the ourse or not. That's why I ended up taking a lab course and decided to work on QLever. Indecision aside, I thought working on a real project that people actually use could make me a better software engineer, and maybe even a researcher. Oh boy, was I right.

## Hold on, what is SPARQL?

### Lets start with something simple, SQL

SQL, short for **S**tructured **Q**uery **L**anguage, is a language that allows users to query tabular datasets. I'm pretty sure you're familiar with the concept of SQL since this is probably taught in most of the undergrad studies. But I will try to explain why do we actually need SPARQL.

In SQL databases, you can store the information as tables show below. You can easily see the one has id A was born in X and does H for a living. 

|id   |born   |job   |
|:---:|:---:|:---:|
| A  | X  | H |
| B  | X+1  | J  |
| C  | X+2 | K  |

``` sql
CREATE TABLE Person (id INT, name TEXT, birth_city TEXT);
CREATE TABLE Company (id INT, name TEXT, city TEXT);
CREATE TABLE WorksAt (person_id INT, company_id INT);
```

It is queried like shown below really easy.

```sql
SELECT p.name
FROM Person p
JOIN WorksAt w ON p.id = w.person_id
JOIN Company c ON w.company_id = c.id
WHERE p.birth_city = 'Freiburg' AND c.city = 'Berlin';
```

