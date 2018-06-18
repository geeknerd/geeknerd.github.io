---
layout: post
title: Some of the useful packages for Sublime Text 3
excerpt: "Useful packages for Sublime Text 3, which I found to be a very handy coding text editor not only for programmers but also for everyday users to have a enjoyful typing experience. Well, of course some of the credits goes to the mechanical keyboard I'm using L0L."
date: 2018-01-09
modifited: 2018-01-09
comments: true
pinned: true
tags: [MacOS, Notes]
---
#### ConvertToUTF8 && Codecs33
Best plugins to solve the Chinese random character issues. Some uses GBK Encoding Support, which also does the job the Codecs33 is the root of it.

I don't have the problem of typing in Chinese characters, maybe I had a work-around before but can't remember it now. Haven't tried other languages but should be pretty similar and I think Sublime Text comes with a lot of language supports. 

#### Markdown Editing
Most people might not need this but if you're editing markdown files locally, especially the ones from Github, you're going to need this package for great markdown highlighting. 

The package itself defaults the settings to GFM, which is the GitHub flavored Markdown, and in my user settings I set it pretty close to what ther other files would look, left-aligned, line numbers, black colors, etc. 
{% highlight shell linenos %}
{
    "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
    "wrap_width": 0,
    "draw_centered": false,
    "line_padding_top": 2,
    "line_padding_bottom": 2,
    "line_numbers": true,
    "tab_size": 4
}
{% endhighlight %}

Also, it'll be very useful to have ```tab``` move to the end of the quotes. Put the following keybinding to user defined. 
{% highlight shell linenos %}
[
    // Move out of common paired characters () and [] with `Tab`
    {
        "keys": ["tab"],
        "command": "move",
        "args": {"by": "characters", "forward": true},
        "context": [
            // Check if next char matches (followed by anything)
            { "key": "following_text", "operator": "regex_match", "operand": "(:?`|\\)|\\]|\\}).*", "match_all": true },
            // ...and that there is a paid character before it on the same
            // line. This lets you `tab` to Indent at lines with single ]s
            // still, like in a JSOn file
            { "key": "preceding_text", "operator": "regex_contains", "operand": "(:?`|\\(|\\[|\\{)", "match_all": true }
        ]
    },

    // Move out of single and double quotes with `Tab`
    {
        "keys": ["tab"],
        "command": "move",
        "args": {"by": "characters", "forward": true},
        "context": [
            { "key": "following_text", "operator": "regex_match", "operand": "(?:\"|').*", "match_all": true },

            { "key": "preceding_text", "operator": "regex_contains", "operand": "(?:\"|')", "match_all": true }
        ]
    }
]
{% endhighlight %}
**6/18/18 UPDATE**
{: .notice}
Markdown Editing failed to work on 3176 with some of the md files and I have turned to Markdown Extended package for editing markdowns and it has been working great so far. 
#### Anaconda + Python 3
There are tons of Python packages that utilize ST3 into a fully customizable Python IDE to use. I tried a few of them but most of the others failed my esthetic expectation with unnecessary coloring of the codes and weird icons. But definitely try those out if fancy is your style. I will stick with these two for Python coding and developing and so far they have met all my needs. 
#### LaTeX-cwl + LaTeXTools
Technically, I would prefer latex editing in Vim or dedicated LaTeX editors like texmaker. However, Texmaker is starting to consume too much of my computer resource, although adequate, and I tried ST3 for Latex editing and it turned out to be just as convenient. Also, half the credit needs to go to PDF Expert for Mac which automatically reloads any edited PDFs, so ST3 only need to build the file and PDF Expert will be able to refresh it. 