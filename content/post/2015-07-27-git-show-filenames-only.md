---
title: Git show filenames only
author: Jon Kuperman
type: post
date: 2015-07-27T17:00:50+00:00
url: /git-show-filenames-only/
categories:
  - Git

---
Sometimes, especially when you have multiple developers working on the same codebase it&#8217;s nice to get a list of just the filenames that were changed in the last commit or even in your current dirty branch.

Fortunately, Git makes this super easy with the **&#8211;name-only** flag. It goes like this:

### Show filenames from the last commit

<pre class="lang:sh decode:true ">git show --name-only</pre>

### Show filenames from the changes yet to be committed

<pre class="lang:sh decode:true ">git diff --name-only</pre>

Hope that helps!