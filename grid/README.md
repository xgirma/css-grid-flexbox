# Grid

NOTE: use Flexbox for UI elements, but Grid for major layout.

# class name 
Grid, each cell has a unique class name. Because now we have to specify in two dimension. If two cell have the same name, they will overlap.

| <img width="500" alt="screen shot 2018-04-21 at 11 47 52 pm" src="https://user-images.githubusercontent.com/5876481/39092262-c654eb4c-45be-11e8-9585-31654f7414c0.png"> |
|:--:| 
| *Flexbox: non-unique class name* |

| <img width="500" alt="screen shot 2018-04-21 at 11 47 14 pm" src="https://user-images.githubusercontent.com/5876481/39092261-b7469150-45be-11e8-9272-82f2f873c12a.png"> | 
|:--:| 
| *Grid: unique class name* |
    
# 01 grid 
We have grid container and grid item. The parent here is the wrapper and the cells (col1, ...) are the children. 

    grid-gap: space between grid cells
    
|<img width="500" alt="screen shot 2018-04-22 at 12 01 59 am" src="https://user-images.githubusercontent.com/5876481/39092362-067f0bc4-45c1-11e8-9c86-1876a01c1f04.png">|
|:--:|
|*grid*|
    
    em Relative to the font-size of the element (2em means 2 times the size of the current font)
    
|<img width="500" alt="screen shot 2018-04-22 at 12 06 07 am" src="https://user-images.githubusercontent.com/5876481/39092364-0c59cf7a-45c1-11e8-9dbd-3c6da96c2cec.png">|
|:--:|
|*example*|

# 02 grid-column

|<img width="500" alt="screen shot 2018-04-21 at 11 25 52 pm" src="https://user-images.githubusercontent.com/5876481/39092148-6fe0a290-45bb-11e8-874d-5b4bd9be15d7.png">|
|:--:|
|*grid-column*|

|<img width="500" alt="screen shot 2018-04-22 at 12 11 02 am" src="https://user-images.githubusercontent.com/5876481/39092398-b55636a4-45c1-11e8-9077-142ce6cd5de8.png">|
|:--:|
|*example*|

# 03 grid-row


|<img width="500" alt="screen shot 2018-04-22 at 12 18 45 am" src="https://user-images.githubusercontent.com/5876481/39092439-cfeeea32-45c2-11e8-86e4-fc74ed0ed303.png">|
|:--:|
|*Grid column and row*|

|<img width="500" alt="screen shot 2018-04-22 at 12 18 59 am" src="https://user-images.githubusercontent.com/5876481/39092440-d51cb8fe-45c2-11e8-9e96-b727d992d77c.png">|
|:--:|
|*Example*|


# 04 media query

    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
|<img width="364" alt="1" src="https://user-images.githubusercontent.com/5876481/39092705-dc76aaaa-45c8-11e8-95c7-d504d6af3cf7.png">| 
|:--:| 
|*<600 px*|

```css
@media (min-width: 650px) { 
	header {
		grid-column: 1 / 2;
		grid-row: 2 / 3;
	}
	article {
		grid-column: 1 / 2;
		grid-row: 1 / 2;
	}
	aside {
		grid-column: 2 / 3;
		grid-row: 1 / 3;
	}
}
``` 

|<img width="600" alt="2" src="https://user-images.githubusercontent.com/5876481/39092706-e0d95002-45c8-11e8-81da-ded309ba7f46.png">| 
|:--:| 
|*>600 px*|

```css
@media (min-width: 1000px) { 
	header {
		grid-column: 2 / 3;
		grid-row: 1 / 2;
	}
	article {
		grid-column: 2 / 3;
		grid-row: 2 / 3;
	}
	aside {
		grid-column: 1 / 2;
		grid-row: 1 / 3;
	}
}
```
|<img width="1200" alt="3" src="https://user-images.githubusercontent.com/5876481/39092709-e5369876-45c8-11e8-81b6-b20e5e3d89b7.png">| 
|:--:| 
|*>1000 px*|

# 05 grid area
The below `css` gives the same result as the above pictures. 

```css
.wrapper {
    display: grid;
    grid-gap: 2em;
    grid-template-columns: auto;
    grid-template-rows: auto;
    grid-template-areas:
            "header"
            "article"
            "aside";
}

header {
    background-color: greenyellow;
    grid-area: header;
}

article {
    background-color: #ff4e4e;
    grid-area: article;
}

aside {
    background-color: darkolivegreen;
    grid-area: aside;
}

@media (min-width: 650px) {
    .wrapper {
        grid-template-columns: 2fr 1fr;
        grid-template-rows: auto;
        grid-template-areas:
                " article article aside"
                "header header aside";
    }
}

@media (min-width: 1000px) {
    .wrapper {
        grid-template-columns: 1fr 5fr;
        grid-template-rows: auto;
        grid-template-areas:
                "aside header header header header"
                "aside article article article article";
    }
}
```

# 06 nesting

```css
.wrapper {
    display: grid;
    grid-gap: 2em;
    grid-template-columns: auto;
    grid-template-rows: auto;
    grid-template-areas:
            "header"
            "article"
            "aside";
}

header {
    background-color: greenyellow;
    grid-area: header;
}

article {
    background-color: #ff4e4e;
    grid-area: article;
    display: grid;
    grid-template-columns: auto;
    grid-gap: 1em;
}

.inner {
    background-color: white;
}

aside {
    background-color: darkolivegreen;
    grid-area: aside;
}

@media (min-width: 650px) {
    .wrapper {
        grid-template-columns: 2fr 1fr;
        grid-template-rows: auto;
        grid-template-areas:
                " article article aside"
                "header header aside";
    }
    .nested {
        display: grid;
        grid-gap: 1em;
        padding: 0.5em;
        border-radius: 0.5em;
        grid-template-columns: repeat(3, 1fr);
    }
}

@media (min-width: 1000px) {
    .wrapper {
        grid-template-columns: 1fr 5fr;
        grid-template-rows: auto;
        grid-template-areas:
                "aside header header header header"
                "aside article article article article";
    }
    .nested {
        display: grid;
        grid-gap: 1em;
        padding: 0.5em;
        border-radius: 0.5em;
        grid-template-columns: repeat(4, 1fr);
    }
}
```

|<img width="360" alt="1" src="https://user-images.githubusercontent.com/5876481/39093539-ec4cc95c-45d5-11e8-87e5-f1718e35ff88.png">|
|:--:|
|*<600*|


|<img width="500" alt="2" src="https://user-images.githubusercontent.com/5876481/39093540-ec5ea3de-45d5-11e8-93ce-c3950ee74e8d.png">|
|:--:|
|*>600*|

|<img width="1000" alt="3" src="https://user-images.githubusercontent.com/5876481/39093541-ec704ed6-45d5-11e8-8cfd-6ffe0865e01e.png">|
|:--:|
|*>1000*|