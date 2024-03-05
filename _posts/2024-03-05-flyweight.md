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

```php
class FizzBuzz {
    private $nums;

    public function __construct($nums) {
        $this->nums = $nums;
    }

    public function getResult() {
        return array_map(function ($num) {
            $output = '';

            if ($num % 3 == 0) $output .= 'Fizz';
            if ($num % 5 == 0) $output .= 'Buzz';

            return $output ?: $num;
        }, $this->nums);
    }
}

$nums = range(1, 3);
$fizzBuzz = new FizzBuzz($nums);
$result = $fizzBuzz->getResult();

print_r($result);
```

Onwards to Flyweight!