# Homework 1

## Introduction

Throughout this homework I tried to incorporate different interesting features of AIML v2:

- `<condition>` + `<li>`: for if-elseif-else statements
- `<think>`: To suppress output for setting variables.
- `<request>`: To get historical user responses for exchanges.
- `<topic>`: To allow conditional recognition of some exchanges, based on a given context.
- `<button>`: To create buttons that direct the user to helpful content.
- `<image>`: To post images of Carl Rogers alongside Rogerian responses for a little unique flair and and to have a little fun with the assignment :), but additionally to establish a little more connection and association between the bot and the user.

## Requirements

- Greet the user, **use the user name in greetings if the user declares it**
- Conduct a conversation of at least **three exchanges across two topics**.
- Support at least **5 different questions per topic**. 
- **When it doesn't understand** the topic the chatbot behaves like a **Rogerian psychotherapist**. 

## Greetings

Greetings are in the section marked:

```xml
<!--***********-->
<!-- GREETINGS -->
<!--***********-->
```

In that section there is a distinction made between when the user provides their name and when they do not. 
It is expected for the user to greet the bot like so `Hello I am *`, where `*` is the users name. 
When the bot is greeted *with* the user's name it will respond randomly between two canned responses.

```
User: Hello I am Charles
helloworldchatbot: How are you doing Charles? Well I hope! My name is helloworldchatbot
```

If the bot is greeted *without* the user's name (i.e. `Hello` or `Hi`), the bot will still introduce itself, this time without incorporating the user's name since it wasn't provided in either of its two canned random responses.

```
User: Hi
helloworldchatbot: Hi! My name is helloworldchatbot.
```

## Setting the topics for discussion

There is a special mechanism I employ to set the topics in the section marked:

```xml
<!--*******************************-->
<!-- SETTING TOPICS FOR DISCUSSION -->
<!--*******************************-->
```

Topics for discussion are presented like so `Hey let us talk about *`, where the value of `*` is set to a variable, `topicrequest`.
There is a `<condition>` tag employed to field various values and the else condition, reserved for unrecognized topics, yields a Rogerian response as required.

Recognized topic:
```
User: Hey let us talk about the weather
helloworldchatbot: Sure let's talk about the weather!
```

Unrecognized topic (bot response is appended by an image of Carl Rogers then embedded as button text):
```
User: Hey let us talk about blogs
helloworldchatbot: So what do you love about blogs? How does it make you feel?
```
## Topics

There are two main supported topics: 

1. Weather
2. Coffee

Each topic has a section with 5 questions:

```xml
<!-- *********** -->
<!-- 5 Questions -->
<!-- *********** -->
```

And each question is marked with a comment to signify the question number (i.e. `<!-- Q1 -->` up to `<!-- Q5 -->`).

Within a topic the three levels of exchange are as follows:

1. Initial Question and initial bot response
2. User says `That was not helpful`, triggering a topic-specific exchange on three specific questions. If the user doesn't previously ask one of those three questions the bot does not recognize it and gives a Rogerian response, else the bot reaches out to Google to answer the questions.
3. Exchange 3 is common across topics, if the user previously said `That was not helpful`, and the user's current response to the bot's Google query is `No` or `Yes` there is a final response that reflects the answer given by the user.

Here is an example exchange:

```
# Exchange 1 - Ask 1 of the 3 recognized questions in the given topic for followup exchanges.
User: How long do you think the sunny weather will last
helloworldchatbot: If I was a betting bot... which I am too simplistic to be ... I would say 5ish months or so.

# Exchange 2
User: That was not helpful
helloworldchatbot: I'm sorry you didn't like that answer. Would a google search be more helpful? <<BUTTON THAT LINKS TO GOOGLE SEARCH>>

# Exchange 3
User: No
helloworldchatbot: I'm sorry I don't think I can help you with this.
```

At each exchange there is the ability for a Rogerian response if the response from the user is not recognized within the given context. This precludes instances where the actual `<pattern>` is not matchable.