---
layout: post
title: Production-ready fizzbuzz (Part 1.5)
date: 2024-03-03
description: Assembling our God
tags: php design pattern
categories: fizzbuzz
related_posts: false
---

# Refactor, refactor, refactor

As our quest for the ultimate FizzBuzz solution continues, we find ourselves delving deeper into the realms of complexity, scalability, and—dare I say it—object-oriented design. 

In the previous chapter, we witnessed the birth of a simple yet functional FizzBuzz implementation. But alas, management was not appeased. They yearned for more. And so, with a deep breath and a hint of trepidation, we embark on Chapter 1.5 of our odyssey: the transition to object-oriented perfection.

```php
class FizzBuzz {

    public function __construct(
        private array $numbers
    ) {}

    public function getAnswer() {
        return array_map(function ($num) {
            $output = '';

            if ($num % 3 == 0) $output .= 'Fizz';
            if ($num % 5 == 0) $output .= 'Buzz';

            return $output ?: $num;
        }, $this->numbers);
    }
}

$numbers = range(1, 3);
$fizzBuzz = new FizzBuzz($numbers);
$answer = $fizzBuzz->getAnswer();

print_r($answer);
```

Behold, the culmination of our efforts, encapsulated within the confines of a class named FizzBuzz. No longer shall our code languish in the squalor of procedural obscurity; it shall ascend to the lofty heights of object-oriented elegance.

Gone are the days of loose arrays and function calls. Instead, we embrace the order and structure afforded by class-based instantiation. The functionality remains the same and our program is just a bit more complex. We define our array, instantiate the class 

Stay tuned for Chapter 2, where we shall unveil our first design pattern: the Flyweight.