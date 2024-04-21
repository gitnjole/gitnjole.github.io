---
layout: page
title: LaraJobs
description: a job posting website built using the Laravel framework
img: assets/img/projects/lara-jobs.png
importance: 2
category: Laravel
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

The application is in a working form right now, but it will get more developed as I get more time to improve it.
I've had a few suggestions for making this project better, so come back later to see if I've finished it!

**Company banners** have been implemented and logos are now permanent throughout your listings!
- ~~Users need to post their company logo every time they post a job which gets very tedious and storage consuming. I could refine this so that users need to post a company logo which would be permanent throughout their account listings (but changeable), and if they wish they can post additional 'banners' on their listings to customize the look of the listing~~

**Redefined User-Listings relations!** Now, company data will be permanent throughout listings so you don't have to insert same data every time!
- ~~The user is currently essentially the company, with the field 'name' synonymous with the name of their company. However, this setup can lead to confusion and inefficiencies. To address this, I plan on investing time in redefining the database structure to allow for discrete, precise attributes for users and companies. Additionally, it's important to eliminate the need to retype the company name every time a listing is posted, along with location/company description, etc.~~

**User showcase:** 
- Users have the option to create their own "willing to work" listings so that employers may get in contact with possible employees, rather than restricting it to just job advertisements. In order for the website to know what to show you based on your account type, I would need to rewrite the home page and make a number of other adjustments (for instance, if you're a company, you might not want to see other companies listing jobs, but you might be interested in seeing people offering their skills).

**Direct apply through application:** 
- May imitate LinkedIn's capability of emailing a CV file and a brief message to the company mail. It is also possible to create custom questions. For instance, users can be required to respond to a question like, "How many years of experience do you have with X?"

**API Integration**
- Currently only supports a simple GET request to view all active listings. Planned expansion of API integration includes creating a new resource through a request.

Example JSON response:
```json
[
    {
        "id": 1,
        "listable_type": "App\\Models\\Company",
        "listable_id": 5,
        "title": "Aut sequi error culpa amet et et.",
        "tags": "laravel, api, js",
        "banner_path": null,
        "description": "Aspernatur impedit ea a eum consequuntur molestias. Reprehenderit pariatur est quibusdam optio itaque quos iste. Qui ex reprehenderit est voluptatum officia. Odio odio cupiditate quo sint et voluptatem quaerat. Sit deleniti ratione doloremque vero animi optio qui.",
        "created_at": "2024-04-21T15:58:52.000000Z",
        "updated_at": "2024-04-21T15:58:52.000000Z"
    },
    {
        "id": 2,
        "listable_type": "App\\Models\\Company",
        "listable_id": 8,
        "title": "Et architecto quam voluptatem expedita et voluptas aut.",
        "tags": "laravel, api, js",
        "banner_path": null,
        "description": "Ipsum rerum enim eveniet possimus aut. Voluptatum qui nulla quia fugit velit qui hic eius. Inventore architecto ea mollitia laudantium veritatis quia. Autem et repellat fugiat debitis error et. Dolor totam quod nesciunt ut est dolor rem. Adipisci nisi provident expedita aut. Voluptatem molestias eligendi aliquid quo animi. Optio maxime sint optio et. Temporibus qui modi dignissimos in optio omnis vitae.",
        "created_at": "2024-04-21T15:58:52.000000Z",
        "updated_at": "2024-04-21T15:58:52.000000Z"
    }
]
```

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

### Companies table
```sql
CREATE TABLE
  `companies` (
    `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT,
    `name` varchar(255) NOT NULL,
    `password` varchar(255) NOT NULL,
    `location` varchar(255) NOT NULL,
    `email` varchar(255) NOT NULL,
    `contact_email` varchar(255) NOT NULL,
    `logo_path` varchar(255) DEFAULT NULL,
    `website` varchar(255) DEFAULT NULL,
    `created_at` timestamp NULL DEFAULT NULL,
    `updated_at` timestamp NULL DEFAULT NULL,
    PRIMARY KEY (`id`),
    UNIQUE KEY `companies_name_unique` (`name`),
    UNIQUE KEY `companies_email_unique` (`email`)
  ) ENGINE = InnoDB AUTO_INCREMENT = 11 DEFAULT CHARSET = utf8mb4 COLLATE = utf8mb4_unicode_ci
```

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

Only listing-related data is stored in the listings table. It is not necessary to post a banner with your listing; in the event that you do not have one, your company logo will be shown. To ensure some consistency across postings, the default Larajobs logo is displayed if you haven't uploaded a custom logo.

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
        $companyListings = Listing::where('listable_type', 'App\Models\Company')
                                ->latest()
                                ->filter($request->only('tag', 'search'))
                                ->simplePaginate(6);

        $userListings = Listing::where('listable_type', 'App\Models\User')
                                ->latest()
                                ->filter($request->only('tag', 'search'))
                                ->simplePaginate(2);
    
        return view('listings/index', [
            'companyListings' => $companyListings,
            'userListings' => $userListings
        ]);
    }
```

This method allows me to access the latest listings along with their respective creator. As the project grows I will have to do further research in optimising fetching all that data as I fear with complexity comes sluggish performance.

That's it for now! If you have any questions or would like to discuss the project with me, you can see the [source code](https://github.com/gitnjole/lara-jobs) or you can reach out to me directly! You can find my contact information on the [about](https://gitnjole.github.io/) page.