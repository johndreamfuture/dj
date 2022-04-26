[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Intro to Django

So far we've learened how to make the back-end for web applications two different ways: in Express with Node in JavaScript, and then with Flask in Python. Both are relatively lightweight and require other libraries in order to have even basic functionality (such as Mongoose or PeeWee). Django is philosophically different in that it strives to be a full-featured *framework*, so it will include significantly more features and have much stronger "opinions" on how its code should be written. Neither philosophical approach (lightweight vs. full-featured) is intrinsically better than the other as both have advantages and disadvantages. You may find yourself prefering one way over the other.

Let's learn the core features of Django and how to build web apps "the Django
way."

## Objectives

By the end of this, you should be able to:

* Discuss the core features of Django
* Compare and contrast building applications with Django and Express
* Walk through how Django handles the request-response cycle

## What is Django?

As defined in the [official documentation](https://www.djangoproject.com/), "Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of Web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source."

Django is a web framework that is know for its speed, security, scalability and versatility. It also comes with a lot of extra features that, although may have a learning curve when it comes to becoming familiar with using them, make your life as a developer a lot easier, eliminating a lot of the hard coding you may have had to do in the past to implement the same functionality.

### Background

Created in 2003 by Adrian Holovaty and Simon Willison, developers at the Lawrence Journal World Newspaper, Django was born out of frustrations the developers had working with PHP. Working for the publication, applications often had to be created very quickly, sometimes within a few hours, and Holovaty and Willison needed a tool to accomplish just that, while keeping the development process clean and maintainable. They wanted to move from PHP to building with Python, but none of the tools and technologies that were around at the time came with the features they wanted - things like CSS, well designed URLs, the way the request/response cycle would work, and deployment. 

Although the initial intention may not have been to create a new web framework, Django proved itself to be an extremely useful and dynamic tool, and the World Company (who owned the newspaper) agreed to open source it. And the rest is history!

### Companies Using Django

Several companies have subscribed to the magic of Django, including many that you may have heard of like Instagram, Spotify, YouTube, The Washington Post, The Guardian, The Onion, Bitbucket, Dropbox, Eventbrite and Prezi.

What are the benefits that these companies see in building their applications with the popular framework?

1. It's highly customizable - new features are easy to implement, giving every application the ability to be unique and stand out.
1. It's scalable - the dream of any business is to grow. When an application is built with Django, the framework doesn't have to change in order for it's size to expand with the business.
1. It's simple and fast - apps can get off the ground faster because the structure is simple, and and Django has a reputation to be quick for development.

Instagram is the largest Django application out there right now. When it was sold to Facebook, they had a total of 13 employees working on the app. Today, they have hundreds!

## Additional Resources

* https://www.djangoproject.com/start/

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
