/// admonition | Some title
Some content
///

/// admonition | Some title
    type: warning

Some content 
///

- &#32;
    ```
    a fenced block
    ```

Definition
: &#32;
    ```
    a fenced block
    ```
> ```
  a fenced block

> with blank lines
  ```

```{.python .extra-class #id linenums="1"}
import hello_world
print("just checking)
```
``` python3
def fizz_buzz(value):
    if(value % 3 == 0 and value % 5 == 0):
        return "FizzBuzz"
    elif (value % 3 == 0):
        return "Fizz"
    elif(value % 5 == 0):
        return "Buzz"
    else:
        return value
```
=== "Tab 1"
    Markdown **content**.

    Multiple paragraphs.

=== "Tab 2"
    More Markdown **content**.

    - list item a
    - list item b
