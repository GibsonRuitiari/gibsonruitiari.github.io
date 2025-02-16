## Let’s Build an SQL Engine

Have you ever run an SQL query and wondered what happens behind the scenes? How does your favorite SQL engine take something as simple as:

```sql
SELECT * FROM users WHERE name = 'JANE';
```

and magically returns the right results? This series is going to describe exactly how that happens and how to implement a modest SQL Engine.

Now you might be cracking your head, scratching it and wondering why would I want to do that? Well, besides being an incredibly fun challenge, 
it's a fantastic learning opportunity! You'll get hands-on experience with: 
Parsers, Lexical Analyzers, Compilers, Finite Automaton, B+ Trees - basically everything 😃!. Also, you get a chance to do something fun!

<aside>
⚠️

If you are not familiar with SQL or need a refresher, I would highly recommend going through this [Quick Reference](https://www.sqltutorial.org/) 
or any other tutorial on the subject. There is going to be no introduction into SQL in this series. You only need to know the basics to continue.

</aside>

## Series Breakdown

This particular series can be broken down as follows:

1. Let’s Build an SQL Engine!
2. SQL Engine, Prologue:  SQL Grammar
3. SQL Engine, Part 1: Lexical Analysis
4. SQL Engine, Part 2: Parser
5. SQL Engine, Part 3: Semantic Analysis
6. SQL Engine, Part 4:  Query Execution

By the end of this journey, you'll have a working SQL engine that can parse, validate, and execute queries—all built from scratch, without external libraries!

## Next Up

I hope you're as excited as I am! This journey will be packed with valuable concepts and hands-on coding. Even though we'll be using Kotlin, 
the ideas here are applicable to any programming language. 