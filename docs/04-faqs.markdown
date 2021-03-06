FAQs
====

Maybe not "frequently asked", but hopefully these answers will be useful.

[TOC]

Should I use d for my project?
------------------------------

If you want lots of control over the resulting documentation: no.

If you want to hook in API docs and such: no.

If you want to write in something other than Markdown: no.

If you have a large project and need more than one level of organization for
your documentation: no.

If you have a small project and want to quickly write some docs that don't look
like ass: **yes!**

Web Servers and File Layout
---------------------------

### Do I need to do anything special with my webserver?

Your webserver should add a trailing slash to directories.  Most sane ones do
that by default these days, so you should be all set.

If you're using a server that doesn't, you might need to add a rewrite rule so
URLs like `/foo` redirect to `/foo/`.

### Why does d use page/index.html instead of page.html?

`d`'s goal is to be quick, easy, and get out of your way.  Most web servers will
serve the folder structure `d` creates sanely without any extra configuration.

This also lets you type links such as `[installation guide](/installation/)`,
instead of requiring you to add the `.html`.

### Can I serve the documentation at a URL other than /?

Sure.  You'll need to use relative links in your content pages though:

    :::markdown
    See the [installation guide][ig] for more information.

    [ig]: ../installation/


### Why can't I use <base\> to have normal-looking links?

The `<base>` tag is a clusterfuck.  Just add the dots.  Trust me.

### Can I reorder the pages?

Sure, make the filenames start with numbers and a dash, like this:

    :::text 
    01-installation.markdown
    02-usage.markdown

`d` will order the files properly, but ignore the number when creating the
URLs, so you still get nice links like `/installation/`.

### Can I create multiple folders/sections?

No, use a different tool.

Page Content
------------

### Can I add a Google Analytics script?

Sure.  Remember that Markdown lets you add raw HTML anywhere.  Just put the HTML
in `footer.markdown` and you're all set.

### Can I add media?

Not yet, but it's on my radar.

### Can I display a table of contents for a single page?

Put `[TOC]` wherever you want it to appear.  It will parse the headings in the
document, remove the first level (the page title) and output a nice list for
you.

### Can I have syntax highlighting for code snippets?

Yep, just put `:::lang` at the beginning of your code blocks, like this:

    :::text
    :::python
    for i in range(10):
        print i

### Can I add HTML into the <head\> of the docs?

Not yet, but it's on my radar.


Writing Tools
-------------

### How can I preview the documentation locally?

You need a real web server to preview the generated files effectively.  Luckily,
you already have one: Python comes with a built-in server that's great for
viewing local files.

Build your docs, then in a separate terminal:

    :::bash
    cd myproject/docs
    cd build
    python -m SimpleHTTPServer

Now open <http://localhost:8000> and view your docs!

### Can I make d auto-rerender when my files change?

Yes, use [kicker](https://github.com/alloy/kicker) to watch for changes and run
`d`.

### Kicker is only for OS X, what about Linux?

I haven't found a tool like kicker for Linux, sorry.

Let me know if you write one -- I've wanted it for a while now.

### Can I write in something other than Markdown?

No, use a different tool.

### Can I add auto-generated documentation into d's docs?

No, auto-generated docs are a cop out.  Sit down and write some real,
hand-crafted documentation for humans.

### Can I output to PDF/ePub/man pages/etc?

No, use a different tool.

### Can I make a "theme" for d?

No, use a different tool.
