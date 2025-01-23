---
layout: page
title: Todo BE
description: A baseline Symfony project showcasing my current level of expertise.
img: assets/img/projects/todo-be.png
importance: 4
category: Symfony
---

# Currently in development

This Symfony application showcases my current level of expertise in PHP and web development.  Key features include:

- Web UI: View your tasks, perform CRUD operations through a user-friendly web interface.
- Standard CI/CD practices showcased such as writing tests, deployment through Docker

## Current Functionality

- Web Interface: The foundation of the web UI is in place, providing the ability to view basic card details.
- API Endpoint: Working on allowing API approach to editing or fetching notes for a given user

### Project structure

```bash
src/
├── Controller         # Handles HTTP requests and responses
│   ├── SecurityController.php
│   ├── TaskController.php
│   └── UserController.php
├── Entity             # Database entity definitions
│   ├── Task.php
│   └── User.php
├── Form               # Form type definitions
│   ├── RegistrationType.php
│   └── TaskType.php
├── Repository         # Database query repositories
│   ├── TaskRepository.php
│   └── UserRepository.php
├── Security           # Authentication and authorization
│   ├── AppAuthenticator.php
│   └── TaskVoter.php
└── Service            # Business logic services
    ├── TaskService.php
    └── UserService.php
```
## Currently working on:

`SESSIONS`
- [x] Implement basic functionality
- [ ] Implement session web controller
- [ ] Implement API controller
- [ ] Implement RabbitMQ for periodic task deletion

`WEB-UI`
- [x] Refactor web layout and design

Working out the design in free time. Least concerning, but would be nice to have componentised session cards.


That's it for now! If you have any questions or would like to discuss the project with me, you can see the [source code](https://github.com/gitnjole/todo-be) or you can reach out to me directly! You can find my contact information on the [about](https://gitnjole.github.io/) page.
