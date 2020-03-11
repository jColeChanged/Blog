---
layout: post
title: Eliza is Only a Chat Bot
published: true
---

I&rsquo;m reading through <a href="http://norvig.com/paip.html">Paradigms of
Artificial Intelligence: Case Studies in Common Lisp</a> and finding it to be
 amazing. <a href="http://norvig.com/index.html">Peter Norvig</a>, formerly of
NASA and now head of research at Google, has a way of talking AI programs that
shaped the field in their time in a way that makes me feel as if I get what is
going on.

Its weird though. He does present the material in a brilliant fashion, but
at the same time the programs he is talking about are like magic.

You know, they seem baffling and astounding. Then you find out what is
<a href="http://www.youtube.com/watch?v=2H81A3bU68k">really going on</a> and
it might still be cool, but its a different kind of cool. Once you know
the trick behind it, the entire program is seen in a new light.

To show you what I mean I&rsquo;m going to go over an AI that Norvig talks
about in the book called Eliza. Eliza is a chat bot built way back when and it
tricked a lot of people into thinking there was actually something intelligent
behind it. That people took it seriously actually freaked out the person who
coded the AI.

So what is Eliza? Eliza is a rule based translator. What does that mean?
Well I&rsquo;ll give you an example of a set of rules to show you. These rules
are taken directly from an implementation of a subset of the features of the
actual Eliza that I wrote in Clojure, one of my favorite programming languages.
I&rsquo;m hoping it will be pretty readable even if you aren&rsquo;t
familiar with the language:

```
("?*x I want ?*y"
  ("What would it mean if you got ?*y"
   "Suppose you got ?*y soon?"
   "Why do you want ?*y"))
```

So what we have above is a list of two items. The first item is a string and
the second item is a list. That first string, it is a pattern. Whenever Eliza
is told something it will check this rule and look at the pattern. It will then
try to see if there is any point in what it was told where &lsquo;I want&rsquo;
appears. If there is it will save segments of text which will be called
`?*x` and `?*y` for use. The second item in the list is
another list. This list contains strings, each of which is a response. If Eliza
managed to save anything to `?*x` and`?*y` it will
select one of these response strings at random. Then using the saved variables
it will create a new string. There is also this stage where Eliza converts
things like you to me and me to you in the values it saves. So given this rule
if I were to tell Eliza, &ldquo;Hey you, I want to make you look simple.&rdquo;
It might respond, &ldquo;What would it mean if you got to make me look
simple.&rdquo;

Eliza has a lot of rules and most of them are kind of vague. It allows you to
become convinced that it knows more than it really does by being vague. It
parrots things back, but leaves things open ended. Sometimes it is going to
mess up and give really weird responses, but with enough patterns it can lead
you into fooling yourself for a while.

Fun fact: at one point Eliza almost got a job. Prestigious medical journals
were actually wondering if using Eliza to fill in for actual psychiatry might
be a good idea. They wouldn’t have to pay it much after all. Remember when I
said the author was a little bothered by how seriously people were taking the
program? I wonder what sort of things might have brought that on.

Despite all of this, it was actually pretty cool to implement. Usually I
would use regular expressions to match a pattern in a string, but this time I
got to see how matching patterns can be done at a lower level. Now if
you&rsquo;re interested in all of that you can check out some of the code in
a <a href="https://gist.github.com/2970757">github gist</a>. Be
warned&hellip;. I&rsquo;m using mutually recursive functions and there are a
whole lot of parentheses.