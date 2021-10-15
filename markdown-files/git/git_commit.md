# Creating the Perfect Commit in Git

A commit in Git can be one of two things:

- It can be a jumbled assortment of changes from all sorts of topics: some lines of code for a bugfix, a stab at rewriting an old module, and a couple of new files for a brand new feature.
- Or, with a little bit of care, it can be something that helps us stay on top of things. It can be a container for related changes that belong to one and only one topic, and thereby make it easier for us to understand what happened.

In this post, we’re talking about what it takes to produce the latter type of commit or, in other words: the “perfect” commit.

- **Part 2:**  Branching Strategies in Git\
  _Coming soon!_
- **Part 3:**  Better Collaboration With Pull Requests
- **Part 4:**  Merge Conflicts
- **Part 5:**  Rebase vs. Merge
- **Part 6:**  Interactive Rebase
- **Part 7:**  Cherry-Picking Commits in Git
- **Part 8:**  Using the Reflog to Restore Lost Commits

### [](https://css-tricks.com/creating-the-perfect-commit-in-git/#why-clean-and-granular-commits-matter)Why clean and granular commits matter

Is it really necessary to compose commits in a careful, thoughtful way? Can’t we just treat Git as a boring backup system? Let’s revisit our example from above one more time.

If we follow the first path – where we just cram changes into commits whenever they happen – commits lose much of their value. The separation between one commit and the next becomes arbitrary: there seems to be no reason why changes were put into one and not the other commit. Looking at these commits later, e.g. when your colleagues try to make sense of what happened in that revision, is like going through the “everything drawer” that every household has: there’s everything in here that found no place elsewhere, from crayons to thumbtacks and cash slips. It’s terribly hard to find something in these drawers!

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/50a0193efca449639e21176d21db334c~tplv-k3u1fbpfcp-zoom-1.image)

Following the second path – where we put only things (read: changes) that belong together into the same commit – requires a bit more planning and discipline. But in the end, you and your team are rewarded with something very valuable: a clean commit history! These commits help you understand what happened. They help explain the complex changes that were made in a digestible manner.

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e1b18b86d2654170b6d3774463197d9e~tplv-k3u1fbpfcp-zoom-1.image)

How do we go about creating better commits?

### [](https://css-tricks.com/creating-the-perfect-commit-in-git/#composing-better-commits)Composing better commits

One concept is central to composing better commits in Git: the **Staging Area**.

The Staging Area was made exactly for this purpose: to allow developers to select changes – in a very granular way – that should be part of the next commit. And, unlike other version control systems, Git forces you to make use of this Staging Area.

Unfortunately, however, it’s still easy to ignore the tidying effect of the Staging Area: a simple `git add .` will take *all* of our current local changes and mark them for the next commit.

It’s true that this can be a very helpful and valid approach sometimes. But many times, we would be better off stopping for a second and deciding if really *all* of our changes are *actually* about the same topic. Or if two or three separate commits might be a much better choice.

In most cases, it makes a lot of sense to keep commits rather smaller than larger. Focused on an individual topic (instead of two, three, or four), they tend to be much more readable.

The Staging Area allows us to carefully pick each change that should go into the next commit:

```
$ git add file1.ext file2.ext
```

This will only mark these two files for the next commit and leave the other changes for a future commit or further edits.

This simple act of pausing and *deliberately choosing* what should make it into the next commit goes a long way. But we can get even more precise than that. Because sometimes, even the changes in a *single file* belong to multiple topics.

Let’s look at a real-life example and take a look at the exact changes in our “index.html” file. We can either use the “git diff” command or a Git desktop GUI like [Tower](https://www.git-tower.com/?utm_source=csstricks&utm_medium=guestpost&utm_campaign=the-perfect-commit):

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9b08fdd18d134b798bd8a17347e2fb07~tplv-k3u1fbpfcp-zoom-1.image)

Now, we can add the `-p` option to `git add`:

```
$ git add -p index.html
```

We’re instructing Git to go through this file on a “patch” level: Git takes us by the hand and walks us through all of the changes in this file. And it asks us, for each chunk, if we want to add it to the Staging Area or not:

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/39b8216435614c9a94e54a4d7f9b70ac~tplv-k3u1fbpfcp-zoom-1.image)

By typing `[Y]` (for “yes”) for the first chunk and `[N]` (for “no”) for the second chunk, we can include the *first* part of our changes in this file in the next commit, but leave the other changes for a later time or more edits.

The result? A more granular, more precise commit that’s focused on a single topic.

### [](https://css-tricks.com/creating-the-perfect-commit-in-git/#testing-your-code)Testing your code

Since we’re talking about “the perfect commit” here, we cannot ignore the topic of testing. How exactly you “test” your code can certainly vary, but the notion that tests are important isn’t new. In fact, many teams refuse to consider a piece of code completed if it’s not properly tested.

If you’re still on the fence about whether you should test your code or not, let’s debunk a couple of myths about testing:

- **“Tests are overrated”** : The fact is that tests help you find bugs more quickly. Most importantly, they help you find them before something goes into production – which is when mistakes hurt the most. And finding bugs *early* is, without exaggeration, priceless!
- **“Tests cost valuable time”** : After some time you will find that well-written tests make you write code faster. You waste less time hunting bugs and find that, more often, a well-structured test primes your thinking for the actual implementation, too.
- **“Testing is complicated”** : While this might have been an argument a couple of years ago, this is now untrue. Most professional programming frameworks and languages come with extensive support for setting up, writing, and managing tests.

All in all, adding tests to your development habits is almost guaranteed to make your code base more robust. And, at the same time, they help you become a better programmer.

### [](https://css-tricks.com/creating-the-perfect-commit-in-git/#a-valuable-commit-message)A valuable commit message

Version control with Git is not a fancy way of backing up your code. And, as we’ve already discussed, commits are not a dump of arbitrary changes. Commits exist to help you and your teammates understand what happened in a project. And a good commit message goes a long way to ensure this.

But what makes a good commit message?

- A brief and concise subject line that summarizes the changes
- A descriptive message body that explains the most important facts (and as concisely as possible)

Let’s start with the subject line: the goal is to get a brief summary of what happened. *Brevity*, of course, is a relative term; but the general rule of thumb is to (ideally) keep the subject under 50 characters. By the way, if you find yourself struggling to come up with something brief, this might be an indicator that the commit tackles too many topics! It could be worthwhile to take another look and see if you have to split it into multiple, separate ones.

If you close the subject with a line break and an additional empty line, Git understands that the following text is the message’s “body.” Here, you have more space to describe what happened. It helps to keep the following questions in mind, which your body text should aim to answer:

- What changed in your project with this commit?
- What was the reason for making this change?
- Is there anything special to watch out for? Anything someone else should know about these changes?

If you keep these questions in mind when writing your commit message body, you are very likely to produce a helpful description of what happened. And this, ultimately, benefits your colleagues (and after some time: you) when trying to understand this commit.

On top of the rules I just described about the *content* of commit messages, many teams also care about the *format*: agreeing on character limits, soft or hard line wraps, etc. all help to produce better commits within a team.

To make it easier to stick by such rules, we recently added some features to [Tower, the Git desktop GUI](https://www.git-tower.com/?utm_source=csstricks&utm_medium=guestpost&utm_campaign=the-perfect-commit) that we make: you can now, for example, configure character counts or automatic line wraps just as you like.

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4698581ed8241da845b16fe02740ad6~tplv-k3u1fbpfcp-zoom-1.image)

### [](https://css-tricks.com/creating-the-perfect-commit-in-git/#a-great-codebase-consists-of-great-commits)A great codebase consists of great commits

Any developer will admit that they want a great code base. But there’s only one way to achieve this lofty goal: by consistently producing great commits! I hope I was able to demonstrate that (a) it’s absolutely worth pursuing this goal and (b) it’s not *that* hard to achieve.

If you want to dive deeper into advanced Git tools, feel free to check out my (free!) [“Advanced Git Kit”](https://www.git-tower.com/learn/git/advanced-git-kit?utm_source=csstricks&utm_medium=guestpost&utm_campaign=the-perfect-commit): it’s a collection of short videos about topics like branching strategies, Interactive Rebase, Reflog, Submodules and much more.

Have fun creating awesome commits!
