With rvest.

## HTML
![[Pasted image 20240321134131.png|300]]
First, we assign the document to a variable
```r
html <- read_html(html_document)
```
Then, we can get the parts we want.
Be aware of the difference between nodes(html_elements) and text(html_text).
```r
html %>% html_children() %>% html_text()
```
Navigating through the nodes can be done like this
```r
html %>% html_elements('div') %>% html_elements('p')
```
or like this
```r
html %>% html_elements('div p')
```
The attributes can be identified as
```r
html %>% html_element('a') %>% html_attr('href')
```

Scrape a table using
```r
html <- read_html(table_html) # table with <th> header cells
html %>% html_table(header = TRUE)
```


## CSS

![[Pasted image 20240321140452.png]]
### Type Selectors
So
```r
html %>% html_elements('h1, p')
```
And also type selectors
```r
type1, type2{
key: value;
}
html %>% html_elements('type1, type2')) # e.g. 'h1' or 'a' or 'span' or *
```

Depending on how many HTML elements of the same type there are on a web page, CSS selectors will return a different number of nodes.

### Classes
They are identified with a dot.
Note the difference between .class1.class2 which select elements with both classes
and .class1 , .classe2 which selects elements with class1 OR class2.

### IDs
Identified with a #
There should be only one unique ID, but if you add also the class, it enhance the readibility of the selector.

### Pseudo-classes



### CSS Combinators
Structure: `h2#someid {space|>|+|~} .someclass`

space : Descendant combinator
\> : Child combinator : for DIRECT descendant
\+ : Adjacent sibling combinator : returns only the next sibling
~ : General sibling combinator : ??



## XPATH

XML Path Language.
Select nodes on properties of other nodes.

Syntax: axes, steps, and predicates 
Axes: / or // 
Steps: HTML types like span and a 
Predicates: `[...] ` to select only nodes with certain properties
Example: `//span/a[@class = "external"] (CSS: span > a.external )`
Example: `//*[@id = "special"]//div (CSS: #special div or *#special div )`


