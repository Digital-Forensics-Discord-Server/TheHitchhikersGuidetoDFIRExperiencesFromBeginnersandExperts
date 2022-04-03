{sample: true}
# Chapter Two

Writing in Markdown is easy! You can learn most of what you need to know with just a few examples.

To make *italic text* you surround it with single asterisks. To make **bold text** you surround it with double asterisks.

## Section One

You can start new sections by starting a line with two # signs and a space, and then typing your section title.

### Sub-Section One

You can start new sub-sections by starting a line with three # signs and a space, and then typing your sub-section title.

## Including a Chapter in the Sample Book

At the top of this file, you will also see a line at the top that says `{sample: true}`, immediately above the # Chapter Two title. This means that when you generate a preview of your book, or publish a new version of your book, this chapter will be included in a separate sample book that will be created. When you publish your book, this will give potential readers a sample book to read, when they are deciding whether they want to buy your book.

## Links

You can add web links easily. Here is a link to the [Leanpub homepage](https://leanpub.com).

When you are creating a web link, the part between the square brackets [ ] contains the words that people will see in your book, and the part in the round brackets ( ) is the web address you are linking to.

## Images

You can add an image to your book in a similar way.

First, add the image to the "resources" folder for your book. You will find the "resources" folder in your book's "manuscript" folder, which is at the top level of your book's folder in GitHub or Bitbucket. 

If you look in your book's "resources" folder right now, you will see that there is an example image there with the file name "palm-trees.jpg". Here's how you can add this image to your book:

![Palm Trees](palm-trees.jpg)

As this example image shows, **on a line by itself** you type an exclamation point !, followed by the image caption between square brackets and the filename between round brackets.

To learn more about adding images, see [this link](https://leanpub.com/markua/read#images).

## Lists

### Numbered Lists

You make a numbered list like this:

1. kale
2. carrot
3. ginger

### Bulleted Lists

You make a bulleted list like this:

* kale
* carrot
* ginger

## Code Samples

You can add code samples really easily. Code can be in separate files (a "local" resource) or in the manuscript itself (an "inline" resource).

### Local Code Samples

Here's a local code resource:

{format: ruby}
![Hello World in Ruby](hello.rb)

### Inline Code Samples

Inline code samples can either be spans or figures.

A span looks like `puts "hello world"` this.

A figure looks like this:

```ruby
puts "hello"
```

You can also add a caption:

{caption: "Hello World in Ruby"}
```ruby
puts "hello"
```

To learn more about adding code samples, see [this link](https://leanpub.com/markua/read#code).

## Tables

You can insert tables easily inline, using the GitHub Flavored Markdown (GFM) table syntax:

| Header 1  | Header 2 |
| --- | --- |
| Content 1 | Content 2 |
| Content 3 | Content 4 Can be Different Length |

To learn more about adding tables, see [this link](https://leanpub.com/markua/read#tables).

## Math

You can easily insert math equations inline using either spans or figures.

Here's one of the kinematic equations `d = v_i t + \frac{1}{2} a t^2`$ inserted as a span inside a sentence.

Here's some math inserted as a figure.

{caption: "Something Involving Sums"}
```latexmath
\left|\sum_{i=1}^n a_ib_i\right|
\le
\left(\sum_{i=1}^n a_i^2\right)^{1/2}
\left(\sum_{i=1}^n b_i^2\right)^{1/2}
```

To learn more about adding math, see [this link](https://leanpub.com/markua/read#math).

## How Book.txt Works

If you look in your book's "manuscript" folder, you will see there is a file called "Book.txt".

The "Book.txt" file is what our book generators use to decide what other files to include in your book. It is a list of the files in your "manuscript" folder that you decide you want to include in your book.

You can have multiple chapters in one file, but we recommend one chapter per file. This way, it's easier to navigate.

If you open the "Book.txt" file now, you will see the following list:

chapter1.txt
chapter2.txt
chapter3.docx
chapter4.docx

If you want to write in plain text, you should delete the following lines in the "Book.txt" file, and save the change:

chapter3.docx
chapter4.docx

(Those files are for people who want to write in Word, not in plain text.)

Now, the only two lines listed in the "Book.txt" file will be:

chapter1.txt
chapter2.txt

The next time you create generate a preview of your book, our book generators will only use the "chapter1.txt" and the "chapter2.txt" files, because they are the only files listed in the "Book.txt" file. Our book generators will ignore any files in your "manuscript" folder that are not listed in the "Book.txt" file, even if those other files are still in the "manuscript" folder.

## Creating a Preview of Your Book

You can generate a new version of your book any time by going to the "Preview" page for your book on Leanpub.

To go to the Preview page for your book, click on the Versions tab on Leanpub when you are working on your book. By default you will be taken to the "Preview New Version" page, which is where you'll be able to preview your book.

## Getting Help

Finally, to get help, go to the Help tab for your book in Leanpub and then either...

1. See our Getting Started page to learn how to get started.
2. See our Getting Help page to learn how to get help.
3. Clicking the link to the [Markua manual](https://leanpub.com/markua/read) on the Getting Help page. The Markua manual contains everything you need to know about writing in Markdown on Leanpub. (Our dialect of Markdown is called Markua.)

By the way, that was how you make a numbered list in Markdown.

You can also make a bulleted list like this:

* item one
* the second item
* another item

We hope that you find writing in Markdown on Leanpub to be simple and enjoyable!
