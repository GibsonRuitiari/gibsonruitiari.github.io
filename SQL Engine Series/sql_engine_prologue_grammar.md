# SQL Engine, Prologue:  SQL Grammar

Before we start building our SQL Compiler and Engine, we first need to understand how SQL statements are structured. 
This means defining the rules that determine how an SQL statement should be written.


## Grammar Definition

A grammar is a set of rules that are used to specify the syntax of a programming language. 
In other words, grammar consists of a bunch of rules that tells us how to arrange words and symbols for a particular language, 
such as SQL, in a way that makes sense.

![Confused unga bunga🫤](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExdGVjc3AyOHJyZjFzcmllcmV2N3lmc2lsOWRscnRscmw0dzVnempleSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/Wgb2FpSXxhXLVYNnUr/giphy.gif)

To make sense of this, think of the English language. When you are writing an English Sentence, you follow specific rules, albeit implicitly.
For example, a simple English sentence consists of a: Subject and Verb. So a sentence can be expressed using the following rule.

```
        <sentence> → <subject> <verb> "."
```

The `<sentence>` can be considered as a **rule**, the ` → ` is read as **is described as** and the `<subject>` & `<verb>` 
can be read as **non-terminals** whose values are yet to be given.

In other words, the '<sentence>' rule consists of a `<subject>` followed by a `<verb>` and it is finishes 
with a terminal symbol '.'.

Just like English SQL too has its own formal grammar that specifies how SQL statements are to be written. 
For example, a simple select statement can have the following form:

```
            SELECT name FROM users
```
That is _give me names from the name column present in the users table_.

If you keenly think about it, in a select statement we need to specify the columns we want and the table to work on. 
Therefore, we can denote the columns we want as `<column_list>` and the table to be `<table_name>`. 
From this, we can come up with a structure for a basic select statement, that can be expressed as follows:

```
           <select_statement> → SELECT <column_list> FROM <table_name>
```
The above `<select_statement>` can be termed as a 'rule' or 'production', and the words '**SELECT**' and '**FROM**' can be termed as terminals. 
On the other hand, the `<column_list>` and `<table_name>` can be termed as non-terminals.

In simplistic terms, the `<select_statement>` rule consists of '**SELECT**' keyword followed by a `<column_list>`, 
then followed by a '**FROM**' keyword, which is then followed by `<table_name>`.

![it makes senseee 😌](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExZmRydWZldjV3NDZpbzdvY3E1ZmF0anV4d2xwYnlqOGNveGxtY2RxYyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xT9DPr4VjeCgeiLoMo/giphy.gif)


Now that we know what grammars are, let’s take a closer look at their components.

## Components of Grammar

We have already introduced the components of a grammar, albeit fleetingly. As a restatement, a grammar can be thought of as a collection of symbols. The symbols can be categorized as either:

1. terminal;
2. non-terminal;
3. production/rule,; and
4. start-symbol

### Terminal

A terminal is an elementary or basic symbol of a language; a symbol that is generally fixed and that appears as it is in 
the compiled form of the language. In other words, terminals are those symbols that won’t undergo further processing by the compiler.

Terminals generally represent actual strings like '**hello**', numbers like **123**, operators such as '**!=**', '**==**'
'**>**', '**AND**', and a language’s keywords such as '**for**' & '**while**'.

SQL, just like any other language has its own keywords, such as '**FROM**', '**SELECT**', '**WHEN**'. As an example, 
the `<select_statement>` rule, the words '**FROM**' & '**SELECT**' are terminals because they are keywords.

```
       <select_statement> → SELECT  <column_list>  FROM  <table_name>
```
### Non-Terminal

A **non-terminal** is an abstract symbol representing a **rule** in a language. It can be **expanded** into a combination 
of **terminals** and **other non-terminals**. Non-terminals do **not** appear directly in the final compiled output; 
instead, they are replaced by their expanded forms.

For example, in the `<select_statement>` rule, `<column_list>` and `<table_name>` are **non-terminals** because they **expand** into 
other rules rather than being fixed symbols.

For instance, the complete definition of the `<column_list>` rule is:
```
              <column_list> → “*”
```

whereas for the `<table_name>` rule, it is:
```
              <table_name> → “users”
```

Thus, the compiled version of the `<select_statement>` rule would be:
```
               SELECT * FROM users
```

### Production/Rule

A **rule** (also known as a **production**) consists of:

- A **name**, referred to as the **head**.
- An **arrow** (**→** or **::=**), which means "is described as."
- A **sequence of terminal and non-terminal symbols**, which form the body of the rule.

The **head** represents the **name of the rule** and is sometimes called the **Left-Hand Side (LHS)**.

The **Right-Hand Side (RHS)** consists of a combination of **terminal** and **non-terminal symbols**, and these two form the **definition** of the rule.
It is important to note that sometimes, the RHS can consist of either a **terminal** or **non-terminal symbols**, such a rule is still completely defined.
```
                    <table_name>    →      “users”
                    <-- Head -->          <-- Body/Description -->
                    Left Hand Side        Right Hand Side                             
```

### Start Symbol

A start symbol is the top level rule that represents the complete structure of a language. For instance, going back to 
our sentence rule, we can describe English language's sentence structure as follows:
```
              <sentence> → <subject> <verb> “."
              <subject> → <determiner> <noun>
              <verb> → “runs”
              <determiner> → “The”
              <noun> → “Cat”
```
