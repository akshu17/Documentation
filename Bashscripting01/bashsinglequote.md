# BASH Scripting Interview Notes

## Escape Character (), Single Quotes (' ') vs Double Quotes (" ")

------------------------------------------------------------------------

## 1. What is an escape character in BASH?

The escape character (`\`) removes the special meaning of a character
and treats it literally.

Example:

``` bash
echo "Price is \$100"
```

Output:

    Price is $100

------------------------------------------------------------------------

## 2. Why do we use backslash ()?

-   Escape special characters
-   Continue command on next line
-   Print characters literally

Example (line continuation):

``` bash
echo "This is a long command \
that continues on next line"
```

------------------------------------------------------------------------

## 3. Difference between single quotes and double quotes

  Feature                Single Quotes    Double Quotes
  ---------------------- ---------------- ----------------
  Variable expansion     No               Yes
  Command substitution   No               Yes
  Escape characters      No               Yes
  Literal text           Always literal   Mostly literal

------------------------------------------------------------------------

## 4. Single quotes behavior

Everything inside single quotes is treated as literal text.

``` bash
name="John"
echo 'Hello $name'
```

Output:

    Hello $name

------------------------------------------------------------------------

## 5. Double quotes behavior

Variables and commands are expanded.

``` bash
name="John"
echo "Hello $name"
```

Output:

    Hello John

------------------------------------------------------------------------

## 6. Escaping characters inside double quotes

``` bash
echo "She said \"Hello\""
```

Output:

    She said "Hello"

------------------------------------------------------------------------

## 7. Escaping single quote workaround

``` bash
echo 'It'\''s Linux'
```

Output:

    It's Linux

------------------------------------------------------------------------

## 8. When to use single quotes

-   Exact literal text
-   No variable expansion
-   Safer for special characters

------------------------------------------------------------------------

## 9. When to use double quotes

-   When using variables
-   Preserve spaces
-   Command substitution needed

------------------------------------------------------------------------

## 10. Clear difference example

``` bash
var="world"

echo 'Hello $var'
echo "Hello $var"
```

Output:

    Hello $var
    Hello world

------------------------------------------------------------------------

## 11. Common escaped characters

-   \$

-   "

-   '

-   \

-   -   

-   ?

------------------------------------------------------------------------

## 12. Command substitution example

``` bash
echo "Today is $(date)"
```

Works in double quotes only.

------------------------------------------------------------------------

## 13. Best practices

-   Use single quotes for fixed strings
-   Use double quotes for variables
-   Always quote variables

Good practice:

``` bash
echo "$filename"
```

------------------------------------------------------------------------

## End of Notes
