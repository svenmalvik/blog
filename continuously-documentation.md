# The beauty of continuous documentation.
For many, writing documentation is as exciting as traveling collectively in the morning; we'd rather avoid it. Maybe it's because we think no one will ever read what we're writing. We think so when we sit down and write, demotivated and tired, so what we write is of course boring and dry.


I have long been interested in publishing a book. A few years ago, I interviewed Nilanjan Raychaudhuri, the author of "Scala in Action". We had lunch together in the cafeteria at Nordea. He led a Scala workshop I attended. "How much time did you spend on writing this book?" I asked. "About two years. You need to have great discipline," he replied. Joe, I knew that writing a book is challenging, but hearing it directly from someone who has published a book that I have read and, as many others read, it was exciting! Perhaps he can tell how I'm getting bored most quickly, can do the same to write a book. I may be able to write 3, 4 months before I get bored.


According to the popular and well-known personality test Myers-Briggs Type Indicator (MBTI), which describes 16 different personality types, I am type INTP. This means, among other things, that I love to start new projects, but I rarely quit these just because I'm bored. When an INTP has understood the concept behind what it researches or investigates, the project is not exciting anymore. The projects should therefore be limited in time and scope.


In the summer of 2016 I received a fantastic assignment in the project I was working on; I should maintain the system documentation. First and foremost, I had to make sure that developers documented what should be documented. The system documentation is automatically generated and what we eventually get is an html web page. In short. We use javadoc to read the data from the code base, such as comments, codes, and rules and we want to include in the documentation. We use these data afterwards to generate asciidoc files. Finally, these files are converted to html, and present system documentation as a web page


So far nothing is particularly beautiful. But, what if we take it a step further? Choosing a random project from GitHub and generating a Kindle book that is interesting and exciting? I had to try this. I looked at GitHub, and found the perfect project. Then I tested my theory and made my INTP-friendly shortcut to a book.


The "iluwatar / java-design-patterns" project, located on GitHub, describes 100 design patterns. Everything from the "Gang of Four" patents to many other unknown patterns is described here. After a few hours I had the first version of a book on my kindle app. I did not generate to html but to epub, which is an open standard for e-books. From there I converted to Amazon's mobi format as I uploaded to my phone.


I was very pleased! I remember lying in bed that night and reading in the "MIN" book; so cool! It was not perfect, but I knew exactly what had to be changed to get it good. There were a few rounds of changes. In total, there were 4, 5 rounds with javadoc code adjustments, asciidoc and comments in the code base, before I realized that if I wanted to make a book that's good enough for somebody to read it, it needs better and many more Good and understandable comments describing the classes, methods and variables in the code base. Maybe even some pictures explaining what's hard to describe.


## Conclusion:
Documentation is important. In fact, everyone should take good time when it comes to documentation of the code base. Document so that readers understand what the modules, classes, and the solution itself do, and how everything is connected. Images are important to include. The system documentation should always be updated and possibly be part of a Jenkins Pipeline. If we practice continuous documentation in a smooth manner and take documentation seriously from day one in the delivery, we can all become authors.

One last thing. Export your documentation to a format you like to read in, for me it's Kindle.
