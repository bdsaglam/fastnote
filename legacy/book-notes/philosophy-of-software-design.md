
## Chapter 2

Obscurity occurs when important information is not obvious. A simple example is a variable name that is so generic that it doesn’t carry much useful information (e.g., time).
Complexity comes from an accumulation of dependencies and obscurities. As complexity increases, it leads to change amplification, a high cognitive load, and unknown unknowns. As a result, it takes more code modifications to implement each new feature. In addition, developers spend more time acquiring enough information to make the change safely and, in the worst case, they can’t even find all the information they need. The bottom line is that complexity makes it difficult and risky to modify an existing code base.

## Chapter 3

Good design doesn’t come for free. It has to be something you invest in continually, so that small problems don’t accumulate into big ones. Fortunately, good design eventually pays for itself, and sooner than you might think.

It’s crucial to be consistent in applying the strategic approach and to think of investment as something to do today, not tomorrow. When you get in a crunch it will be tempting to put off cleanups until after the crunch is over. However, this is a slippery slope; after the current crunch there will almost certainly be another one, and another after that. Once you start delaying design improvements, it’s easy for the delays to become permanent and for your culture to slip into the tactical approach. The longer you wait to address design problems, the bigger they become; the solutions become more intimidating, which makes it easy to put them off even more. The most effective approach is one where every engineer makes continuous small investments in good design.

## Chapter 4

An abstraction is a simplified view of an entity, which omits unimportant details. Abstractions are useful because they make it easier for us to think about and manipulate complex things.

Interfaces should be designed to make the common case as simple as possible

By separating the interface of a module from its implementation, we can hide the complexity of the implementation from the rest of the system. Users of a module need only understand the abstraction provided by its interface. The most important issue in designing classes and other modules is to make them deep, so that they have simple interfaces for the common use cases, yet still provide significant functionality. This maximizes the amount of complexity that is concealed.

## Chapter 5

Beware of `Temporal Decomposition`; when designing modules, focus on the knowledge that’s needed to perform each task, not the order in which tasks occur.

Information hiding and deep modules are closely related. If a module hides a lot of information, that tends to increase the amount of functionality provided by the module while also reducing its interface. This makes the module deeper. Conversely, if a module doesn’t hide much information, then either it doesn’t have much functionality, or it has a complex interface; either way, the module is shallow.

When decomposing a system into modules, try not to be influenced by the order in which operations will occur at runtime; that will lead you down the path of temporal decomposition, which will result in information leakage and shallow modules. Instead, think about the different pieces of knowledge that are needed to carry out the tasks of your application, and design each module to encapsulate one or a few of those pieces of knowledge. This will produce a clean and simple design with deep modules.


## Chapter 6
General-purpose interfaces have many advantages over special-purpose ones. They tend to be simpler, with fewer methods that are deeper. They also provide a cleaner separation between classes, whereas special-purpose interfaces tend to leak information between classes. Making your modules somewhat general-purpose is one of the best ways to reduce overall system complexity.

Questions to ask yourself:
What is the simplest interface that will cover all my current needs? If you reduce the number of methods in an API without reducing its overall capabilities, then you are probably creating more general-purpose methods. The special-purpose text API had at least three methods for deleting text: backspace, delete, and deleteSelection. The more general-purpose API had only one method for deleting text, which served all three purposes. Reducing the number of methods makes sense only as long as the API for each individual method stays simple; if you have to introduce lots of additional arguments in order to reduce the number of methods, then you may not really be simplifying things.

In how many situations will this method be used? If a method is designed for one particular use, such as the backspace method, that is a red flag that it may be too special-purpose. See if you can replace several special-purpose methods with a single general-purpose method.

Is this API easy to use for my current needs? This question can help you to determine when you have gone too far in making an API simple and general-purpose. If you have to write a lot of additional code to use a class for your current purpose, that’s a red flag that the interface doesn’t provide the right functionality. For example, one approach for the text class would be to design it around single-character operations: insert inserts a single character and delete deletes a single character. This API is both simple and general-purpose. However, it would not be particularly easy to use for a text editor: higher-level code would contain lots of loops to insert or delete ranges of characters. The single-character approach would also be inefficient for large operations. Thus it’s better for the text class to have built-in support for operations on ranges of characters.

## Chapter 7


## Chapter 10
Exceptions don’t occur very often in running systems, so exception handling code rarely executes. Bugs can go undetected for a long time, and when the exception handling code is finally needed, there’s a good chance that it won’t work (one of my favorite sayings: “code that hasn’t been executed doesn’t work”). A recent study found that more than 90% of catastrophic failures in distributed data-intensive systems were caused by incorrect error handling1. When exception handling code fails, it’s difficult to debug the problem, since it occurs so infrequently.

## Chapter 11
I have noticed that the design-it-twice principle is sometimes hard for really smart people to embrace. When they are growing up, smart people discover that their first quick idea about any problem is sufficient for a good grade; there is no need to consider a second or third possibility. This makes it easy to develop bad work habits. However, as these people get older, they get promoted into environments with harder and harder problems. Eventually, everyone reaches a point where your first ideas are no longer good enough; if you want to get really great results, you have to consider a second possibility, or perhaps a third, no matter how smart you are. The design of large software systems falls in this category: no-one is good enough to get it right with their first try.

## Chapter 14

Consistency has three requirements: first, always use the common name for the given purpose; second, never use the common name for anything other than the given purpose; third, make sure that the purpose is narrow enough that all variables with the name have the same behavior.

## Chapter 16

Comments belong in the code, not the commit log.
