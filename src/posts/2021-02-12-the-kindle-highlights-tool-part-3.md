---
title: "The Kindle Highlights Tool, Part 3"
date: "2021-02-12"
categories: 
  - "software-development"
coverImage: "kindle-e1613119249898.jpg"
---

> "This tale grew in the telling."
> 
> J. R. R. Tolkien, foreword to Lord of The Rings

I recently went back to my Kindle Tool, ([Part 1](https://tawanda.dev/posts/2020-08-10-building-my-first-app-a-kindle-reader-highlights-extractor-part-1/), [Part 2](https://tawanda.dev/posts/2020-08-11-the-kindle-highlights-extractor-tool-part-2/)) to try and add more features. I wanted to have to automatically create txt files so I could easily review the highlights.

Firstly I needed to make the a new folder called books to hold all the books. Using fs.mkdir, (and StackOveflow) this was pretty straightforward:

```
const pathName = path.join(__dirname, '/books/');

fs.mkdir(pathName, { recursive: true }, (error) => {
    if(error) {
        console.log('failed to make dir')
    }
    else {
        console.log(`successfully created the dir: ${pathName}`);
    }
});
```

I declared a variable called pathName which is the output folder. I should probably do better error handling, but that's for another day.

I then used Node's fs.appendFile() method to create the txt files by looping through the books array. I could have used other methods, like streams or writefile but I took the easy way out.

```
books.forEach((book) => {
        txtFilePath = pathName + book.title + '.txt';
        for (let i = 0; i < book.highlights.length; i++) {
            fs.appendFile(txtFilePath, book.highlights[i] + "\n\n", (error) => {
                if (error) {
                    console.log(error);
                }
            });
        }
    });
```

And voila. That did it. After running my index.js I got a folder called "books" in the root directory. The txt files are stored inside this directory.

I'm really pleased I got this far though I'm not proud of the code. I will definitely continue to refactor and add more features.

I can now easily review my notes and highlights. Hopefully this will make me review more books.

Also the code is now on [Github](https://github.com/tawandamoyo/KindleKlipper). The code is a mess, but I will clean it up soon, as I learn more and add more features.

Dear old Tolkien was right: tales grow in the telling. So does code.
