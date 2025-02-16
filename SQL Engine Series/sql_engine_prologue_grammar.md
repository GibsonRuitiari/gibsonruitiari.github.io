 [[<u>home </u>]](https://gibsonruitiari.github.io/root)


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
The above `<sentence>` rule is structured as follows: A `<subject>` followed by a `<verb>` and it ends with a full-stop `.`.
The `<subject>` consists of `<determiner>` and `<noun>`. On the other hand, the `<verb>` is defined as the word 'runs'.
The `<determiner>` is defined as the word 'The', while `<noun>` is defined as the word 'Cat'.
Putting it all together, when we compile the `<sentence>` rule, we get 'The Cat runs.' 
Take note that `<sentence>` rule is our start symbol, because it is the top level rule that represents the complete structure of 
an English language sentence.

Similarly, the structure for an SQL select statement can be described as follows:
```
          <select_statement> → SELECT  <column_list> FROM  <table_name>
          <column_list> → "*"
          <table_name> → "users"
```
The above `<select_statement>` rule consists of: the `SELECT` keyword followed by a `<column_list>` and `FROM` keyword. 
The rule ends with a `<table_name>`. Expanding the `<column_list>` rule, we find that it consists of `*` which represents all columns.
On the other hand, the `<table_name>` rule consists of the string 'users'.
Also, note that for the SQL select statement structure, the `<select_statement>` is our start symbol.

![It all makes sense noow!](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExOG5nbmt5dWRtczljc3J5ZnVqeTk5ZzI4dWRrbnBlZDFnejVzeGM4MSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xSM46ernAUN3y/giphy.gif)

Having looked at the components of a formal grammar, let’s take a closer look at the notations used to describe them.

## Grammar Notation: Extended Backus Naur Form (EBNF)

By now you might have already noticed that our rules are being written down in a certain way; following a particular notation.
A grammar notation describes the structure of a grammar rule. In other words, grammar notations enable us to linguistically
write our grammar rules. Think of grammar notation as a symbolic representation that enables us to structure our rules.

As an example, in the English language, there are multiple sentence structures. A simple English sentence can be made up of a
```
      Subject + Verb + Object
```
Whereby the `Object` might be option i.e., it might or might not be there. How then do we compactly represent this?

![Hmm hol’ up, hol’ up… 🤔](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExejU5ZTJubjluZ2s4N2ZyYzRtazJ2Y2Rodzl3N3I3ejY2Z2duMXc5cCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/cn7GcSZ1KWqO7CJw1B/giphy.gif)

This is where notations come in. Assume the symbol `[  ]` represents “optional” that is, anything enclosed inside it is optional, 
it can either be there or not. Using this notation, we can describe the above English sentence structure as follows:
```
              <sentence> → <subject> <verb> [<object>]
```
Without notation, expressing the structure of an English sentence compactly can be challenging. 
For this reason, language developers use **notations** to concisely define the **syntactical structure** of their languages.
This discussion will focus on Extended Backus Naur Form (**EBNF**).

### Extended Backus Naur Form (EBNF)

EBNF is a notation for formally and compactly describing the syntax of a language and/or its rules. To compactly write a rule, 
EBNF provides four control forms that apply to the RHS (body of a rule). They are:

1. Sequence → a combination of items from left to right and the order in which the items appear is important. As an example, 
`<subject>` `<verb>` uses a sequence control form because the symbols `subject` and `verb` follow each other sequentially.
2. Choice → this is represented by `|`  and it is where we have a list of items and one is chosen from the list of alternatives.
The order by which items appear is un-important. An example, “The” | “Are” uses the choice control form because the symbols 
“The” and “Are” are alternatives which can be chosen to the exclusion of the other.
3. Option → this is represented by `[  ]` and items enclosed inside the square brackets are optional, that is, they can either be there or not; they can either be included or discarded.
4. Repetition → this is represented by `{   }` and items enclosed inside the curly brackets are repeatable, that is, they can be included 0 or more times.

It is important to note that in EBNF, terminals such as keywords are enclosed inside `“  “`. Thus, any symbol enclosed inside 
“…” is a terminal. As an example `the` is a terminal.

### Application

Applying our knowledge of **EBNF**, we will construct two SQL statement rules: `**SELECT**` and `**INSERT**`. 
This will demonstrate how to define rules using **EBNF notation** effectively. It is important to remember that an **SQL statement** can be either 
a **SELECT** statement or an **INSERT** statement. Therefore, we begin with the **start symbol** `<sql_statement>`, 
which can be represented in notation form as follows:
```
<sql_statement> → <select_statement> | <insert_statement>
```
The `<sql_statement>` rule can consist of either `<select_statement>` or `<insert_statement>`.

The `<select_statement>` rule it can be represented in EBNF notation form as:

```
<select_statement> → “SELECT” <select_list> “FROM” <table_name>  ["WHERE” <condition>] [ "GROUP BY" <column_list>]

<column_list> → <identifier> {"," <identifier>} 

<select_list> → "*" | <column_list>

<identifier> → <letter>|<digit> { <digit>| <letter>| "_"}

<table_name> →  <identifier>

<condition> → <identifier> <comparison_operator> <identifier>

<letter>  → <upper_case> | <lower_case>

<digit>  → '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'

<comparison_operator> → "=" | "!=" | ">" | "<" | ">=" | "<="
```
The `<select_statement>` rule is defined as sequence of `SELECT` keyword, `<select_list>` rule, `FROM` keyword, and `<table-name>`.
The rule ends with two optional constructs: 
 - The `WHERE` keyword and a `<condition>`.
 - The `GROUP BY` keyword and an `<order_list>`.
The `<column_list>` rule is defined as a sequence of `<identifier>`, followed by **zero or more** occurrences of `","` 
and another `<identifier>`. 
The `<select_list>` rule can expand into either the **terminal symbol `"*"`** or the `<column_list>` rule. 
The `<identifier>` rule expands into a single `<letter>` or `<digit>`, followed by **zero or more** occurrences of `<digit>`, `<letter>`, 
or the terminal symbol `"_"`. 
The `<digit>` rule represents **any number from 0-9**, where each digit can be **selected independently** (e.g., you can choose `"0"` while discarding the rest). 
The `<letter>` rule consists of either `<upper_case>` or `<lower_case>` letters
The `<condition>` rule expands into a sequence of:  `<identifier>`, `<comparison_operator>` and `<identifier>`. 
The `<comparison_operator>` rule consists of a set of alternatives, including `"="`, `">"`, and others.

Given the `<select_statement>` rule, an example of an SQL Statement that matches it can be:
```jsx
         SELECT * FROM USERS WHERE AGE > 12  
```
![Agreeed](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExb3dyY3hqMGxqMXZwOWs1Z3c4M3JzZG4xMjNrcWRsb2RzYnVmZnhxbSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/13ZHjidRzoi7n2/giphy.gif)

For the `<insert_statement>` rule it can be represented in EBNF notation form as follows:
```
<insert_statement> → “INSERT INTO” <identifier> “(” <column_list> ")" "VALUES"  "(" <value_list> ")"

<column_list> → <identifier> {"," <identifier>} 

<value_list> → <value> {","<value>} 

<identifier> → <letter> | <digit> { <digit>| <letter>| "_"}

<value> → <sql_literal>

<sql_literal> →  <string> | <number> | <null>

<string> →  '"'<characters>'"' | "'" <character> "'"

<characters> →  <character> |<character><characters> 

<character> →  <digit> | <letter> 

<number> → <integer_part> 

<integer_part> →  <digit>{<digit>} 

<null> →  "null"

<digit>  → '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'

<letter>  → <upper_case> | <lower_case>
```
The `<insert_statement>` rule can be described as a sequence of: `INSERT INTO` keyword, `<identifer>` rule, `(` terminal symbol, `<column_list>` rule, `)` terminal symbol,  `VALUES` keyword, ``(` terminal symbol,
`<value_list`> rule,  and `)` terminal symbol.

On the other hand, the `<value_list>` rule is defined as a sequence of `<value>` followed by **one or more** occurrences of `,` and another `<value>`.
A `<value>` is described by the `<sql_literal>` rule, which can expand into a `<string>`, a `<number>`, or `<null>`. 
A `<string>` expands into a sequence of characters enclosed in either double quotes `" "` or single quotes `' '`. 
The `<characters>` rule expands into either:
    - A single `<character>` chosen from `<digit>` or `<letter>`, or
    - A sequence of `<character>` followed by `<characters>`.
The `<number>` rule expands into `<integer_part>`, which is further expanded into a sequence of digit and repeatable.
The `<null>` rule expands into the terminal symbol `"null"`.

Given the <insert_statement*>* rule, an example of an SQL Statement that matches it can be:
```
 INSERT INTO USERS (NAME, AGE) VALUES ('JOHN', 12)  
```

You may have noticed that **EBNF notation** allows us to **compactly describe** the syntax of **SELECT** and **INSERT** statements—something that would have been difficult to express otherwise.
This demonstrates a key advantage of using **formal notation**, particularly **EBNF**, to define the **syntactical structure** of a language. 
However, an **observant reader** might notice that while we have provided **examples** of SQL statements that conform to our SQL grammar rules, we have not yet **formally proven** their correctness.
Thus, the next section will focus on **proving** that our example SQL statements **match** the rules we have defined.

### Proof Using Derivation Trees
Knowing how to read and write a grammar rule using EBNF notation is one thing—proving that an input conforms to the rule is another.

For example, given the input:  `SELECT * FROM USERS WHERE AGE > 12`, can we demonstrate that a compiler will correctly match it to the rule:
```sql
<select_statement> → "SELECT" <select_list> "FROM" <table_name>  ["WHERE" <condition>] ["GROUP BY" <column_list>]
```

By proving that the input matches this rule, we gain insight into how the compiler processes our grammar rule in relation to the given input.

![https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHZ1YW14cWFoZ2I2M3R2MGtnajg3ejNsdGFuMnRpNnJwbjRvcGViciZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3orieUe6ejxSFxYCXe/giphy.gif](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHZ1YW14cWFoZ2I2M3R2MGtnajg3ejNsdGFuMnRpNnJwbjRvcGViciZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3orieUe6ejxSFxYCXe/giphy.gif)

There are several methods to **prove** that a given input conforms to a grammar rule. One such method—and the focus of this discussion—is the **derivation tree**.

A **derivation tree** (also called a **parse tree**) provides a graphical representation of how an input string is derived from a grammar rule.

- The **root node** of the tree represents the grammar rule being applied.
- The **leaf nodes** contain the actual symbols from the input string.
- The **characters** of these symbols appear at the **bottom** of the tree and are read from **left to right**.

For the rule and input discussed earlier, we can construct the derivation tree as follows:

1. Choose the root node, which in this case is `<select_statement>`;
2. Expand the root node into “SELECT” `<select_list>` “FROM” `<table_name>`, and optionally [”WHERE” `<condition>`] since the “where” part appears in our input
3. Since “SELECT” is a terminal symbol, we go to the next symbol `<select_list>`, thus expand `<select_list>` into "*"  because  the symbol ‘*’ appears in our input. 
Note that we have dropped `<column_list>` because it does not appear in our input.
4. Since “FROM” is a terminal symbol, we go to the next symbol `<table_name>`, we will expand it into `<identifier>`, which is then further expanded into “USERS”. 
Note that the characters “USERS” are a combination of letters thus fitting the description of the `<identifier>` rule;
5. Because the optional [”WHERE” `<condition>`] is included, expand into the “WHERE” `<condition>`
6. Expand the `<condition>` rule into “AGE > 12”

Graphically, this can be represented as:
