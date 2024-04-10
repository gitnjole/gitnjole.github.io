---
layout: post
title: Creating an Editable Card Input UI
date: 2024-03-28
description: My solution to implementing an input inside a moving a card element
tags: js
categories: js-learning
related_posts: false
---

# Initial design

While working on my project [e-charge-tracker](https://github.com/gitnjole/e-charge-tracker) I wanted to have an animated charging card display where the user would be able to enter the card information before checking its status. I came across a Tailwind component for a simple Payment Card Form created by [David Schinteie](https://davidschinteie.hashnode.dev/tailwind-css-creating-a-simple-and-modern-payment-card-form).

Here is his design of the interactable card:
{% include figure.liquid loading="eager" path="assets/gifs/payment-form.gif" class="img-fluid rounded z-depth-1" %}

It looks nice, but the goal was for the user to interact with the card directly and input the details into the image, as opposed to using seperate input fields. In the original version, any click on the card would flip the card over. This was handled by the `toggleBackCard()` function written in JavaScript:

```js
const toggleBackCard = () => {
    cardEl = document.getElementById("creditCard");
    if (cardEl.classList.contains("seeBack")) {
    cardEl.classList.remove("seeBack");
    } else {
    cardEl.classList.add("seeBack");
    }
};
const showBackCard = () => {
    cardEl = document.getElementById("creditCard");
    if (!cardEl.classList.contains("seeBack")) {
    cardEl.classList.add("seeBack");
    }
};
const hideBackCard = () => {
    cardEl = document.getElementById("creditCard");
    if (cardEl.classList.contains("seeBack")) {
    cardEl.classList.remove("seeBack");
    }
};
```

## Creating input fields

First, instead of projecting user entered values onto the card, I added input fields directly onto the card element. That created a problem for me. In the original code, if the user clicked anywhere on the card, it would flip. That function clearly bothered users as they wouldn't be able to insert their data as the card would constatnly flip on them. 

## Conditional flipping

Next, I needed to make the `toggleBackCard` function smarter by implementing a check to see if the click originated from the input field

```js
const toggleBackCard = () => {
    //Stop execution if clicked inside an input field
if (event.target.tagName === 'INPUT') {
    return;
}

const cardEl = document.getElementById("creditCard");
if (cardEl.classList.contains("seeBack")) {
    cardEl.classList.remove("seeBack");
} else {
    cardEl.classList.add("seeBack");
}
};
```

I removed the `onclick` attribute entirely from the card's HTML element.  Then, I added targeted event listeners:

```js
document.getElementById("cardNumber").addEventListener("click", (event) => {
    event.stopPropagation();
});

document.getElementById("ccvNumber").addEventListener("click", (event) => {
    event.stopPropagation();
});
```

The `event.stopPropagation()` is key to prevent click events on the input fields from bubbling up and triggering the flip.

# The result

With these changes, the card animation behaves perfectly! The card flips when a user clicks on a non-input area and the user can freely enter their details without unexpected flips and data loss.

{% include figure.liquid loading="eager" path="assets/gifs/payment-mine.gif" class="img-fluid rounded z-depth-1" %}
