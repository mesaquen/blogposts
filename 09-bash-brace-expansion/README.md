# Bash: Brace expansion

Somewhere in my storage I keep PDF files with random content just for fun,
for about six years now.

The funny thing was, I was revising its owner/group/user permissions and
some of them were with a different permission than the usual.

A simple `chmod` command like the following would do the trick:

```code
chmod 600 file01.pdf file05.pdf file09.pdf
```

But, as a developer, some times we just have that itch to spend 30 minutes
trying a easier way of doing something that usually takes 20 seconds. Just
for the sake of future proof your repo.

To make things challenging I didn't want to update needlessly the files that
would match the pattern `file0*.pdf`. What would I use on this situation?

Since I new exactly which files I needed to update, using `find` regex felt
a bit of overkill for this and quite verbose.

What came in mind to me were two things:

- Brace expansion
- Filename expansion

Both of them would work in a similar way but I chose to use brace expansion
because I was already using it for some brute force scripting in a
cybersecurity project that I was having fun with.

The final command looks like something that resembles this:

```code
chmod 600 file0{5,9}.pdf

# which will expland to: chmod 600 file05.pdf file09.pdf
```
Problem solved. All done!

The cool part about brace expansion is that you have in hands something very
powerful to work with patterns, and progressions.

For instance, if you need to loop through data with leading zeroes from `0000`
to `9999`:

```code
# loop example
for f in {0000..9999}; echo $f; done
```

If you need to follow a pattern, showing only every n-th element you can use
`{0..100..2}`,  in this case it will expand to every even number from 0 to
100, the last portion is how big the step is in this pattern.

Aside from numbers you can also create expansions from letters:

```code
echo a{b,c,d}e
abe ace ade
``` 
There are some limits to what you can do with it, but it is for sure a
powerful tool to know about.
