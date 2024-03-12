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

$numbers = range(1, 30);
$answer = (new FizzBuzz($numbers))->getAnswer();

print_r($answer);
```

Yes, the culmination of our efforts, encapsulated within the confines of a class named FizzBuzz. No longer shall our code languish in the squalor of procedural obscurity; it shall ascend to the lofty heights of object-oriented elegance.

```bash
Array
(
    [0] => 1
    [1] => 2
    [2] => Fizz
)
```
The output remains the same.

Gone are the days of loose arrays and function calls. Instead, we embrace the order and structure afforded by class-based instantiation. Now, behold the evolution of our code: we define our `array`, instantiate the `FizzBuzz` class with it, and elegantly summon the `getAnswer()` method in a single line. The birth of `(new FizzBuzz($numbers))` streamlines our instantiation process, sparing us from the verbosity of traditional class instantiation: 
```php
$fizzBuzz = new FizzBuzz($numbers);
$fizzBuzz->getAnswer();
```

Out humble constructor uses property promotion which prefixes the constructor parameters with `private` which PHP will take as the normal
```php
private array $numbers;

public function __construct()
{
    $this->numbers = $numbers;
}
```

Regarding our `getAnswer` method; Yes, the functionality is exactly the same. I strive for ingenuity here and that is what you will get. Speaking of ingenuity, here is what the spacecraft on mars looks like:

{% include figure.liquid loading="eager" path="assets/gifs/heli_dark.gif" class="img-fluid rounded z-depth-1" %}

Believe it or not, this little robot actually used my FizzBuzz program to determine the wind speeds on Mars. Unfortunately, on January 6th, 2024, the spacecraft met it's untimely end as it crashed into the red sands of Mars. But from its flight emerges a revelation: the upcoming pattern—flight itself!

Stay tuned for Chapter 2, where we shall unveil our first design pattern: the Flyweight.