# Sources
1. Cheat sheets
[Main](https://www.markdownguide.org/cheat-sheet)

2. Editor specific - 
[Visual Studio Code](https://code.visualstudio.com/docs/languages/markdown)

# Summary
## Basic Syntax

---
### Headings
    # H1
    ## H2
    ### H3
    #### and so on...

# H1
## H2
### H3
#### and so on...
---
### Bold
    **bold text**
**bold text**

---
### Italic
    *italic text*
*italic text*

---
### Blockquote
    > line 1

    > line 2
    >> line *3*

> line 1

> line 2
>> line *3*

---
### Ordered List
    1. Item 1
    2. Item 2
    3. Item 3
1. Item 1
2. Item 2
3. Item 3

---
### Unordered List
    - Item 1
    - Item 2
    - Item 3
- Item 1
- Item 2
- Item 3

---
### Code
    Code in a `sentence`
    ```python
    s = "Python code"
    print(s)
    ```
Code in a `sentence`
```python
s = "Python code"
print(s)
```

---
### Horizontal line

    ---
---

---
### Link
    [Google](google.com)
[Google](google.com)

---
### Image
    ![Harambe](https://pbs.twimg.com/media/CsRSv2xWEAEbjK_.jpg)

![Harambe](https://pbs.twimg.com/media/CsRSv2xWEAEbjK_.jpg)

## Extended syntax

---
### Table
    | Column 1 | Column 2 | Column 3 |
    | --: | :--: | :-- |
    | (1,1) | (1,2) | (1,3)|
    | (2,1) | (2,2) | (2,3)|

| Column 1 | Column 2 | Column 3 |
| --: | :--: | :-- |
| (1,1) | (1,2) | (1,3)|
| (2,1) | (2,2) | (2,3)|

---
### Code Block Options

    ```python
    print("1st option")
    ```
    ~~~python
    print("2nd option")
    ~~~
Or you can just indent the text

```python
print("1st option")
```
~~~python
print("2nd option")
~~~
    Or you can just indent the text


---
### Footnotes (unsupported)
    This text requires a footnote[^1], and yet another[^second]
    [^1] First footnote
    [^second] Second footnote

This text requires a footnote[^1], and yet another[^second].

[^1]: First footnote

[^second]: Second footnote

---
### Definition Lists (unsupported)

    First term
    : First definition
    : Second definition

First term
: First definition
: Second definition

---
### Strikethrough

    ~~This is wrong.~~ This is right.

~~This is wrong.~~ This is right.

---
### Task Lists
    - [x] Item done
    - [ ] Item undone

- [x] Item done
- [ ] Item undone






