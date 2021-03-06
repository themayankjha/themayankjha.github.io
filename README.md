## Stux Society. The Internet is a Serious Business
---
Using Jekyll came out after long thinking about what I wanted to accomplish. I wanted to have a blog set up but did not want to pay for any overheads.
I looked for options and came across loads of javascript-based solutions that could easily be deployed with Vercel.

But javascript being javascript scares me to death. I don't know why but javascript tends to be completely understandable and unintelligible at the same time. Hence this site uses the beloved ruby on rails' static site framework 'Jekyll'.

---
### Building the Site
We need to set up the Ruby development environment with jekyll. Since I run Arch pacman is my pakage manager but for other you can easily substitite your own package manager. 
* Install Ruby and Dev packages and then Install Jekyll
```sh
$ sudo pacman -S ruby base-devel
$ gem install jekyll bundler
```
* Clone the theme from [here](https://github.com/artemsheludko/galada.git)
```sh
$ git clone https://github.com/artemsheludko/galada.git
```
* Switch to the cloned folder and run the following
```sh
$ bundle install
$ bundle update
$ bundle exec jekyll serve --livereload
```

Now you have a website up and running on your localhost.

---
### Configuring
The theme has a lot of code that I did not wish to use on this website so I did some cleaning up and removed Disqus comments and added some personalized things here and there.

You are free to use this modified version of the theme instead of the original.

---
#### Copyright

Copyright (c) 2021 [Mayank Jha](https://github.com/themayankjha)

License - [MIT](License.md)

---