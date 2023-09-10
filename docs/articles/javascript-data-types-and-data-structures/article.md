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


::: tabs [data-tabs="1:2"]
::: tab Tab 1
Markdown **content**.

Multiple paragraphs.
:::

::: tab Tab 2
More Markdown **content**.

- list item a
- list item b
:::
:::

![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png | width=100)
![Alt text](https://github.com/ashiquemukkil/1LittleCoderDB/blob/d3ee29e8dbf5a17e1efd951780a7cb9bd3e727f2/imges/precision-pulse-fp16-vs-fp32/fp32.png)


