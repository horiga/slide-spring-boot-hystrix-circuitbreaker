# Landslide

---

# Overview

Generate HTML5 slideshows from markdown, ReST, or textile.

![python](http://i.imgur.com/bc2xk.png)

Landslide is primarily written in Python, but it's themes use:

- HTML5
- Javascript
- CSS

---

# Code Sample

Landslide supports code snippets

    !python
    def log(self, message, level='notice'):
        if self.logger and not callable(self.logger):
            raise ValueError(u"Invalid logger set, must be a callable")

        if self.verbose and self.logger:
            self.logger(message, level)

---

# Code sample w/ Java

    !java
    public static void main(String[] args) throws Exception {
       System.out.pringln("Hello world!");
    }
