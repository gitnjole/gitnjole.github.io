---
layout: page
title: LaraJobs
description: a job posting website built using the Laravel framework
img: assets/img/projects/lara-jobs.png
importance: 2
category: personal
---
This is a simple job posting board built using the Laravel framework. It allows users to post job listings and browse existing listings. Visitors can view job listings and sort them through tags and search filters.

LaraJobs posting board is a web application built on top of the Laravel framework and MySQL database. Leveraging Laravel's migration system, the database schema was created and managed effortlessly. The application follows REST principles, providing clear and intuitive endpoints for performing CRUD operations on job listings.

## Features
- **Job Posting:** Users can create and post job listings.
- **Job Browsing:** Visitors can browse through existing job listings and can directly send an email or view the posting company's website.
- **User Authentication:** Secure user authentication system for creating and managing accounts.
- **Manage Panel:** Features a bare bones admin panel for editing or deleting job listings, along with company name and logo securely.

### Viewing all listings
{% include figure.liquid loading="eager" path="assets/img/projects/layout.png" title="Sample view" class="img-fluid rounded z-depth-1" %}


### Viewing a listing
{% include figure.liquid loading="eager" path="assets/img/projects/show.png" title="Sample view" class="img-fluid rounded z-depth-1" %}

## Installation

Please see my github page for source code and file installation.

[lara-jobs](https://github.com/gitnjole/lara-jobs)

## Further ideas

Currently the application is in the working state, but as I find more time to refine it it will become more fleshed out.
I have a couple ideas for improving this project so you can check back after some time and see if I've done any further work!

**Company banners** have been implemented and logos are now permanent throughout your listings!
- ~~Users need to post their company logo every time they post a job which gets very tedious and storage consuming. I could refine this so that users need to post a company logo which would be permanent throughout their account listings (but changeable), and if they wish they can post additional 'banners' on their listings to customize the look of the listing~~

**Redefined User-Listings relations!** Now, company data will be permanent throughout listings so you don't have to insert same data every time!
- ~~The user is currently essentially the company, with the field 'name' synonymous with the name of their company. However, this setup can lead to confusion and inefficiencies. To address this, I plan on investing time in redefining the database structure to allow for discrete, precise attributes for users and companies. Additionally, it's important to eliminate the need to retype the company name every time a listing is posted, along with location/company description, etc.~~

**User showcase:** 
- Instead of making it purely job listing focused, users could also post their own 'willing to work' listings where companies can reach out to
potential employees. This feature would require me to rewrite the home page and make various tweaks so that the website knows what to display to you based on your account type (for example, if you're a company you might not want to see other companies listing jobs, but you might be interesed in seeing people offering their skills).

**Direct apply through application:** 
- Could mimic LinkedIn features of being able to send a quick message and CV file to the company mail. Can also implement custom questions, for example users would have to answer specific questions like 'How many years of experience do you have with X?'

**API Integration**

## Current database design

### Users table
```sql
CREATE TABLE
  `users` (
    `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
    `email` varchar(255) NOT NULL,
    `password` varchar(255) NOT NULL,
    `logo_path` varchar(255) DEFAULT NULL,
    `company_name` varchar(255) NOT NULL,
    `location` varchar(255) NOT NULL,
    `contact_email` varchar(255) NOT NULL,
    `website` varchar(255) DEFAULT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL,
    PRIMARY KEY (`id`),
    UNIQUE KEY `users_email_unique` (`email`)
  ) ENGINE = InnoDB AUTO_INCREMENT = 2 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_unicode_ci
```

The users table has all user/company information shoved inside and there is no distinction between users and companies. I'm actively researching best practices to seperate them into their own distinct tables so I hope I will be able to finish the change soon. In the most recent update on March 11th I've implemented a somewhat acceptable solution which you can see above.

### Listings table
```sql
CREATE TABLE
  `listings` (
    `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
    `user_id` bigint(20) unsigned NOT NULL,
    `title` varchar(255) NOT NULL,
    `banner_path` varchar(255) DEFAULT NULL,
    `tags` varchar(255) NOT NULL,
    `description` longtext DEFAULT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL,
    PRIMARY KEY (`id`),
    KEY `listings_user_id_foreign` (`user_id`),
    CONSTRAINT `listings_user_id_foreign` FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE CASCADE
  ) ENGINE = InnoDB AUTO_INCREMENT = 2 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_unicode_ci
```

The listings table holds only listing relevant information. Posting a banner with your listing isn't a requirement and if you don't have one your company logo will be used instead. If you haven't uploaded a company logo then the default larajobs logo gets displayed so there is always some form of consistency between listings.

All data is being fetched with Laravel's built in method `with()` so the `index` method looks like this:
```php
    /**
     * Method to show all listings
     *
     * @param Request $request
     *
     * @return \Illuminate\View\View
     */
    public function index(Request $request): \Illuminate\View\View
    {
        $listings = Listing::with('user')->latest()
            ->filter($request->only('tag', 'search'))
            ->simplePaginate(6);
            
        return view('listings/index', [
            'listings' => $listings
        ]);
    }
```

This method allows me to access the latest listings along with their respective `user` data. As the project grows I will have to do further research in optimising fetching all that data as I fear with complexity comes sluggish performance.

That's it for now! If you have any questions or would like to discuss the project with me, you can see the [source code](https://github.com/gitnjole/lara-jobs) or you can reach out to me directly! You can find my contact information on the [about](https://gitnjole.github.io/) page.