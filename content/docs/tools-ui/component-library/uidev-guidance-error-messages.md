---
linktitle: Error Messages
title: O3DE UI Error Messages Guidance and Best Practices
description: Learn how to craft customer-friendly error messages or the O3DE user interface.
toc: true
---

Developing user interface components for Open 3D Engine (O3DE)? Learn how to craft meaningful, useful error messages that will help your users, not frustrate them, by reviewing the principles and best practices in this topic.

### Why write great error messages?

Seriously, why? I mean, the user got an error, right? They can figure out why their code failed or their operation didn't work. They screwed up! We can't possibly tell them how to fix their particular code or implementation running in a specific context, right?

No. No, no, no. In an ideal world, there should be no errors. The customer believes in this utopia, especially if they're using a common workflow. They'd prefer not to acknowledge the idea that the software their success depends on has issues, or that it might not support the way they want to do their work. If they did, they might never use your product!

Great error messages can salve the sting of an unexpected error. Poor ones can lead to negative feedback, or worse: the customer abandons your product and your hard work. Great error messages are little works of **respect** for the user, telling them "yeah, something went wrong. But you know what? We know some things about what happened, and we'd like to try and help you a bit."

Let's look at a pair of examples for the same issue:

```error
ERROR: Cannot complete operation. Maximum range value exceeded.
```

```error
This operation requires positive integer values between 0 and 127. Please choose a value in this range before re-building the scene.
```

The first leads to annoying trial-and-error behavior. The second not only makes it immediately clear to the user what they did wrong, it provides useful preventative guidance about application state and encourages a useful but not-so-obvious practice: making sure all of the values you supplied to the widget are correct before building the scene. You've not only helped the user; you may have saved them future frustration!

Additionally, bespoke and well-designed error messages implicitly communicate an emphasis on quality and user consideration. They're part of the user's perception of the "fit-and-finish" of an application. How did you feel about Windows 10's quality when you encountered an error message like this?

![ALT TEXT HERE](/static/images/tools-ui/windows-10-something-happened-error-message.png)

You probably felt that maybe, just maybe, Windows 10 itself had no idea why it decided to fail, and you probably became a little more skeptical of it as a result.

Error messages, when done poorly, erode trust and increase frustration. Done well, they enable the user to continue work and provide implicit guidance around improved behaviors and code. Good error handling and messages can be a lot of work, but they pay solid dividends:

* Reduced user friction and greater productivity across the product experience
* Training better behaviors in code and UI development and use
* Higher quality and more actionable bug reports
* Better code and UI implementation overall!

No-one ever praises great work in error message design and implementation. But they also don't complain about crappy error messages and consume support resources -- support that would never need to be engaged if we put in the work to craft good error handling mechanisms and well-written error messages.

Let's look at how to write great error messages for O3DE!

### Error Message principles

The most common mistake is wrapping low-level errors and exceptions thrown directly by code and passing them onto the developer or user. Often, this is a function of lazy coding, because very few developers enjoy writing code to filter through the details of a low-level error and massaging it into text that any user or developer can understand. It's enough to debug and unit test your own code, and you know what a NaN error means, right?

That might be true for some forms of software, but O3DE is a tool for builders. Bubbling up an error like `Handle not recognized` to the end user will not make you any friends. So, we need to think about the development of good error messages strategically, and build good code and UI dev practices and habits early.

To start, we'll look at two categories of error message: error messages for code operations, and error messages for application users (UI).

#### Error messages in code

Error messages often begin their life as code-level error descriptions. Many times, these get "passed through" to the end user in a dialog widget or in a console interface. Authoring your error messages well for all audiences, not just technical experts, can simplify your code with regards to the overall customer experience.

* Short messages are better than long ones, but don't skimp on any essential details. Make every word count!
Use basic, proper English grammar. You want to be clear, not clever. More complex phrasing or the use of idioms can make it difficult for non-native English readers, and make localization more difficult.
  * Consistently favor passive voice and pst-tense. "An error occurred..." sounds less judgmental than "We found an error...". Additionally, the error occurred; it is not in the process of occurring. 
* Never, ever pass a low-level error's default description through to the end user. Gather some information programmatically, especially if the default error message would be inscrutable or useless by itself. Every little detail helps.
* Format your error messages for readability and clarity. A little white space or a pair of quotation marks can go a long way in reducing user irritation.
* Don't dump code. The reader can probably see the code in their IDE. It just takes up space and makes the message harder to scan.
* Author your error message for the least technical context (within reason, of course). In most cases, this means a code error that gets raised up to the user interface. Choose the right words to represent that context and avoid "deep code" jargon whenever possible. For example, if an O3DE user sees a message like `STACKOVERFLOWEXCEPTION: SYSTEM STATE UNKNOWN," they will be reasonably alarmed, even if the error is raised from some simple secondary menu recursion code failing. A better choice might be "ERROR: A stack overflow error occurred when updating the menu element tree. Please report this error and restart the application." Consider adding a comment that this message should be rewritten for context if it can appear in the UI.
  * Additionally, avoid "compiler-speak". Use the most viable, least specific terms that describe the error. Focus on the way the user perceives the error, not the compiler or the run-time. For example, saying "ERROR: The operation cannot complete due to unsafe type usage when unmarshalling thread context" is more confusing and concerning than "ERROR: The operation cannot complete as the context cannot be determined. Check to see if any types used to recreate this work are unsafe." This will make it easier for UI writers to craft an appropriate UI-level message, as well.
* Signal next steps -- either taken by the system or for the user to take -- wherever viable. (See the above example.)
* Hints to code definitions can be really helpful in some contexts: "Expected a type `HANDLE_T *` for the first parameter in `ProcessBlobSync()`. `HANDLE_T` is defined as a shared macro in common.h." Remember, though, that this will be inscrutable (and possibly terrifying!) if surfaced through a user interface.
* If the error originates from a third-party library or other binary you don't control, be savvy. Avoid blaming the code, even passively. Just be clear: "The operation could not complete due to a misconfiguration between O3DE and the CoolGraphicsV3 Gem. Please report this issue on GitHub at [link here]."
* Write for the user interface or the IDE, not the command-line!

In simple terms, use empathy. If you were sitting at an IDE building or running this code for the first time, would YOU find this error message clear and helpful, or a bit opaque? Rewrite it until it meets your own "new developer experience" standards. This isn't trivial work, as a consistently poor experience with error messages can erode a user's trust in your code over time.

And remember: it might not be an experienced developer who sees your error message!

#### Error messages in UI components

Writing useful, actionable error messages for end users working in a user interface is an art form. Too often, error messages are passed through from code and not prepared to be read by users who are NOT experienced developers, or even developers at all. Here are some rules to consider when improving error messages for UI users:

* Avoid jargon and technical terms **unless** the context is immediately apparent or if the terminology directly applies to the user's code or actions. Don't introduce new technical ideas that aren't covered in the immediate context. If it is a low-level error and some code or algorithm jargon is unavoidable, provide a clause or a sentence that clarifies it in more accessible terms.
* Describe the error in terms of the action the user took. However, do not **blame** the user. This is a situation where you can use passive voice. For example:
  * BAD: `You entered an incorrect value for Gradient Range.` (active voice)
  * GOOD: `The Gradient Range input field requires a value between 0 and 63.` (passive voice)
* Respect the user's cognitive focus and don't overwrite the error message or provide too much detail. As a simple rule of thumb, aim to keep error messages less than 200 characters **if possible**. Shorter is always better. However, some errors are thorny and may require detailed explication. Try to limit those; or, if the message reflects a composite or aggregated error, format it clearly and use your space to clarify the issues that occurred and any order or causality.
* If the error is a common one, provide a link to a troubleshooting doc, if one exists. Even if they don't click the URL, they will be reassured that the problem is common enough to warrant documentation.
* If the error requires a lot of detail to understand and resolve, request documentation for it.
* Separate messaging from any essential technical details (such as a file name, path, or other programmatic data).

### Error message guidelines

Overall, observe these guidelines when writing error messages at any level:

* Use this pattern: description of error; technical details (optional); next steps or links to further assistance (optional). 
Favor passive voice.
* Be specific.
* Don't use ALL CAPS. Please. Use proper English syntax. 
* Try to keep it under or around 200 characters in most cases. Use good judgment, and always optimize your words.
* Use simple grammar; target an 8th grade reading level.
* Avoid technical jargon in end user UI messages. Be careful with jargon in code-level error messages.
* Focus on the end user's immediate needs, not your own.
* Spellcheck your work!

Here's an example that employs these guidelines, in the context of a user failing to provide correct credentials to a service:

BAD:

```error
ERROR: CREDENTIALS NOT FOUND. WE CANNOT AUTHORIZE YOU.
```

REWRITTEN:

```error
Oops! The password you provided didn't match our records. Can you try again?
```

Here's another example, this time for an error that flows from code to the end user:

BAD (when exposed to devs or an end user):

```error
An error occurred at line 258, col 8 in arglebargle.cpp. Pointer returned null.
```

REWRITTEN AT THE CODE-LEVEL:

```error
An error occurred when the operation received a null pointer. A null pointer is not allowed for the target data when calling RenderToTarget(handle, target, options).

Details:
- File: arglebargle.cpp
- Line: 258
- Column: 8
```

REWRITTEN FOR AN INTERFACE END USER:

```error
Oh no! The target for rendering your scene was not defined. This is a serious error in our code. Please report it at [GitHub link here] and provide any relevant details.
```

Notice how more details were provided for a specific audience, and formatted for clarity? The difference between the originating source error description and what the user finally sees is pretty striking. Always think about **who** might see your error message, and when.

For more reading, check out [Jakob Nielsen's guidance on writing good error messages](https://www.instructionaldesign.org/bad_error_messages/).

### Error Message Best Practices


* Above all else, aim for **clarity**. Ask yourself: "If I got this message while doing my job and I was new to this product or code, what would help me move forward or avoid this error in the future?" Never make the user guess. If you can get further details from the run-time or the existing code, do so, even if it seems tedious. Your extra hour of coding will save your users countless hours in the future. 

* If you are working on developer-focused code (as opposed to user interface code), provide detailed code comments around your error handling and messages. This will help UI error message writers better understand the context and craft better end-user messages.

* Use a natural, friendly voice. Write error messages with empathy, as though you were advising a fellow developer or a new user. It's okay to lead with "Sorry" or "Oops!" if you feel that the error might be in a really disruptive context, but likewise consider localization before you employ sympathetic idioms. All-too-typical "just the developer basics" error strings can feel unnatural and frustrating, especially to developers or users who are learning the product. Cold, severe "programmer" text makes the error feel arbitrary and cryptic, like the user shouldn't even be seeing it in the first place. Make the error feel like what it is: an issue we knew might occur, and that we're alerting you, the user, to **help** you out.

* Avoid hard-coding error messages. Instead, put them in a common JSON (or other format, even CSV or a flat-text model of your own implementation) "dictionary" file and refer to them based on a unique token or handle. This allows for easier review and maintenance without risking build errors or regressions. It also allows for much easier (and thus  significantly cheaper) localization. Document your schema or format for others to easily understand and maintain it.

* Get your error messages reviewed by a technical writer or UX expert! When you open your PR, call out your updated error strings (hopefully in a file specific to error strings, as suggested previously) and request review by someone with technical writing or user interface design experience.
