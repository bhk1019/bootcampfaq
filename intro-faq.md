# Section 1: Portfolio Part 1

## Lesson 2: Installing the Programs

#### Question: 
> Do I have to use Sublime Text 3? Does it matter which kind of text editor I use?

#### Answer:
It shouldn’t matter what kind of text editor you use. Sublime Text 3 is recommended because it is lightweight and easy-to-use, but if you already have a text editor installed on your computer, or a different one that you are more familiar with, feel free to use it. If you run into problems using Sublime, you may try downloading and using a different text editor. Some other commonly used text editors are: Atom, Visual Studio, Brackets, Notepad++.

## Lesson 5: Adding a background

#### Question:
> Why won’t my background image display?

#### Answer:
In order for your background image to display properly, the filename mentioned in the CSS between the `<style></style>` brackets must match the image file present in your directory exactly. Double check that the file names match - in particular, make sure that:
- The filename in your CSS has its extension (like `image.jpg`, rather than just `image`)
- Both filenames have the exact same spelling, including whether the letters are uppercase or lowercase.
- Neither of the files has a doubled extension (like `bg.jpg.jpg`)
- The background image is located in the same folder as your `index.html` file.

#### Question: 
> Does it matter how you indent and space your code?

#### Answer:
Long story short, when the code isn't cleanly indented it can be difficult to read and understand. Indentation of code, in the case of using HTML and Ruby, doesn't change how the code works, but it makes it easier to read. For example, in HTML, indenting after each opening tag, such as `<style>`, makes it easier to see where the closing `</style>` tag is. Indentation won't change how your HTML code behaves, but it will make mistakes like having an opening tag that doesn't have a corresponding closing tag, or similar errors.

## Lesson 8: Coloring the Text

#### Question:
> Why won’t the color of my headings or bio change?

#### Answer:
Double check that the HTML tag has a class, like in `<h1 class=”bio”>` or `<p class=”bio”>`, and that the CSS selector matches the name of the class exactly, as in `.bio { /* properties */ }`. 

## Lesson 13: Go Live

#### Question:
> My website won't display on Netlify, or something on my website doesn't display properly! What do I do?

#### Answer:
It might be an issue specific with Netlify. Go through the following options.
- Make sure that your index page is named exactly: `index.html`, all lowercase.
- If any pictures are not appearing, make sure that the filename of each picture in your zip folder matches the filename of each picture inside of your `index.html` and `style.css` files.
- Try a different web browser.
- Try zipping your entire portfolio over again and uploading a second time.
- Try using [Github Pages](https://pages.github.com/) instead of Netlify.

# Section 2: Ruby

## Lesson 16: Set Up a Coding Environment

#### Question:
> I'm having typing anything using Code Anywhere or Codenvy.

#### Answer:
Try using a different web browser.

## Lesson 17: The Most Important Commands in the Coding Environment

#### Question:
> I get a "command not found" error when I try typing in `cd ..`.

#### Answer:
Make sure you are typing `cd ..` with a space in between the `cd` and the two dots `..`. If you type in `cd..` with no spaces, you will get an error.

#### Question:
> I just made a new folder, or a new file, but I can't find it in the explorer window.

#### Answer:
Try the following things:
- If you are using Codeanywhere: go in the left pane and right click and click the Refresh option in the menu. The folder should become visible.  Alternatively, you could log out and log back into CodeAnywhere to see the folder appear there.

## Lesson 19: Variables and Names

#### Question:
> Why won't the `puts` command work in my program?

#### Answer:
Make sure that when you write a line with `puts` in your program, that you have a variable or string after it without an equals sign in between. For example, write:
```
puts name
```
rather than:
```
puts = name
```

#### Question:
> Why doesn't string interpolation work? When I write `#{name}` the output isn't correct.

#### Answer:
Make sure that the string is surrounded by double quotes, not single quotes. In Ruby, you need to wrap the string in double quotes in order for string interpolation to work.

## Lesson 21: Remainders and Modulo

#### Question:
> Why is it important to know how to calculate the remainder of a number when writing computer programs?

#### Answer:
The modulus operator `%` comes up in many situations in computer programming. Two examples are given below:
- When determining if a number is odd or even.
```
def odd_or_even(num) 
  puts num % 2 == 0 ? "Even" : "Odd" 
end 
odd_or_even(10) 
odd_or_even(11)
```
- When selecting random integers.
```
rand(1000) % 3
```
Check out this link for more reading on the topic: https://betterexplained.com/articles/fun-with-modular-arithmetic/

## Lesson 30: Arrays and Iteration

#### Question:
> When do you use parentheses?

#### Answer:
Parentheses are usually used to pass in arguments to a function. For example, in:
```
is_odd_or_even?(5)
```
we use parentheses after the function `is_odd_or_even?` to denote that we want to use the number `5` as the input for the function. In the Ruby language, many functions do not require you to use parentheses to pass in arguments to a function. Later in the course you will learn which functions require parentheses and which do not.