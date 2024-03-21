---
layout: page
title: The Vault
description: A website for displaying used samples in various songs by artists.
img: assets/img/projects/the-vault.png
importance: 5
category: Core PHP
---

"The Vault" is a PHP-based website dedicated to preserving information on music samples, with a focus on my own music. The server back-end of the project is built entirely in PHP, with Tailwind CSS front-end components added.

This project uses Restful standards and includes a custom router and service container. In its current condition, it is functional; however, please see the 'Further ideas' section for my thoughts on the project's future.

{% include figure.liquid loading="eager" path="assets/img/projects/the-vault.png" title="Main table view" class="img-fluid rounded z-depth-1" %}

## Key Features

- **Sample Documentation:** Capture and catalog information about samples used in music, offering a comprehensive resource for enthusiasts.
- **Artist Selection:** The website exclusively supports samples from chosen artists, ensuring a curated and focused collection.
- **Learning Environment:** "The Vault" serves as a personal training ground, incorporating advanced PHP patterns such as factories, singletons, custom routers, and custom service containers.

## Technology Stack

- **Back-end:** PHP
- **Front-end:** HTML, Tailwind
- **Database:** MariaDB

## On user accessibility

This website is static in its current implementation and does not support adding samples outside of administrator accounts or registering new users. This was done on purpose because the project's objective is to create a web application that communicates with an archive rather than a forum where users may post information. If you are looking at this project as a potential employer, you should check out my [**other projects**](https://gitnjole.github.io/projects/), where I demonstrate my ability to use these kinds of skills. If not, kindly accept the designer's decision. If you would like to develop an open-source version of this project, my code is already ready to handle that feature; it just needs to be written.

## Further Ideas

Currently my bandcamp account is on a waitlist for approval of use of their API so currently data to actual songs is also hard coded into the about page. Eventually there will need to be some amount of refactoring done.
- Refactor controllers to a class in order to adhere to MVC principles more closely
- Fully implement model usage along with User and Sample models
- Simplify the sample inserting process
- Dynamically fetch data from bandcamp to display newly released albums
- Implement sample timestamps using javascript

{% include figure.liquid loading="eager" path="assets/img/projects/samplePage.png" title="Sample view" class="img-fluid rounded z-depth-1" %}

## Database design
### Users table
```sql
CREATE TABLE
  `users` (
    `user_id` int(11) NOT NULL AUTO_INCREMENT,
    `username` varchar(25) NOT NULL,
    `password` varchar(255) NOT NULL,
    `created_at` timestamp NULL DEFAULT current_timestamp(),
    PRIMARY KEY (`user_id`),
    UNIQUE KEY `username` (`username`)
  ) ENGINE = InnoDB AUTO_INCREMENT = 2 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci
```
### Samples table
```sql
CREATE TABLE
  `samples` (
    `sample_id` int(11) NOT NULL AUTO_INCREMENT,
    `artist_name` varchar(100) NOT NULL,
    `song_name` varchar(100) NOT NULL,
    `album_name` varchar(100) DEFAULT NULL,
    `sample_type` enum('drums', 'quote', 'reprise', 'sample') NOT NULL,
    `sampled_artist` varchar(100) NOT NULL,
    `sampled_song` varchar(100) NOT NULL,
    `sampled_album` varchar(100) DEFAULT NULL,
    PRIMARY KEY (`sample_id`)
  ) ENGINE = InnoDB AUTO_INCREMENT = 12 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci
```

### Sample links table
```sql
CREATE TABLE
  `sample_links` (
    `link_id` int(11) NOT NULL AUTO_INCREMENT,
    `sample_link` char(11) DEFAULT NULL,
    `sample_id` int(11) NOT NULL,
    `song_link` char(11) DEFAULT NULL,
    PRIMARY KEY (`link_id`),
    UNIQUE KEY `video_id` (`sample_link`),
    KEY `fk_sample_id` (`sample_id`),
    CONSTRAINT `fk_sample_id` FOREIGN KEY (`sample_id`) REFERENCES `samples` (`sample_id`) ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT `sample_links_ibfk_1` FOREIGN KEY (`sample_id`) REFERENCES `samples` (`sample_id`)
  ) ENGINE = InnoDB AUTO_INCREMENT = 5 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci
```

I felt it was neccessary to seperate samples from their links and YouTube ID's.

### User submissions table
```sql
CREATE TABLE
  `user_submissions` (
    `submission_id` int(11) NOT NULL AUTO_INCREMENT,
    `user_id` int(11) DEFAULT NULL,
    `sample_id` int(11) DEFAULT NULL,
    `created_at` timestamp NULL DEFAULT current_timestamp(),
    PRIMARY KEY (`submission_id`),
    KEY `user_id` (`user_id`),
    KEY `sample_id` (`sample_id`),
    CONSTRAINT `fK_sample_relation` FOREIGN KEY (`sample_id`) REFERENCES `samples` (`sample_id`) ON DELETE CASCADE ON UPDATE CASCADE
  ) ENGINE = InnoDB AUTO_INCREMENT = 8 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_general_ci
```

That's it for now! If you have any questions or would like to discuss the project with me, you can see the [source code](https://github.com/gitnjole/lara-jobs) or you can reach out to me directly! You can find my contact information on the [about](https://gitnjole.github.io/) page.
