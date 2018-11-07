## Git tags
Tags are a simple aspect of Git, they allow you to identify specific release versions of your code. You can think of a tag as a **branch that doesn't change**. Once it is created, it loses the ability to change the history of commits.

### Two Types of Git Tags

There are two types of tags in Git: **annotated** and **lightweight**. Both of them will allow you to refer to a specific commit in a repository, but they differ in the amount of metadata they can store.

#### Annotated Tags

**Annotated tags** store extra **metadata** such as author name, release notes, tag-message, and date as full objects in the Git database. All this data is important for a **public release** of your project.

Tags can also include a more descriptive **tag-message** or **annotation** much like a commit message when you are about to merge. Usually, this is achieved by using (-a for annotation):

```
$ git tag -a v1.0.0
```

Executing this command you will create a new annotated tag identified with version v1.0.0. The command will then open up your commit editor so that you can fill up the metadata.

In case you wanted to add a **tag-message** you can pass the `-m` option, this is a method similar to  `git commit -m.`

```
$ git tag -a v1.0.0 -m "Releasing version v1.0.0"
```

#### Lightweight Tags

**Lightweight tags** are the simplest way to add a tag to your git repository because they store only the hash of the commit they refer to. They are created with the absence of the -a, -s, or -m options and _do not_ contain any extra information.

> Lightweight tags are essentially "bookmarks" to a commit, they are just a name and a pointer to a commit, useful for creating quick links to relevant commits. [By Bitbucket tutorials](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag)

To create a new lightweight tag execute the following command:

```
$ git tag v1.0.0
```

### Additional Commands

**Listing tags** - `git tag`

Use the command whenever you want to list all the existing tags, or you could filter the list with `git tag -l 'v1.1.*'`, where `*` acts as a **wildcard**. It will return a list of tags marked with `v1.1`.

You will notice that when you call `git tag` you don't get to see the contents of your annotations. To preview them you must add `-n` to your command: `git tag -n3`.

```
$ git tag -l -n3
v1.0            Release version 1.0
v1.1            Release version 1.1
v1.2            Release version 1.2
```

The command lists all existing tags with maximum 3 lines of their tag message. By default `-n` only shows the first line.

**Tag details** - `git show <tag_identifier>`

This command presents you with **tag details** and **information** from the commit that was tagged.

```
$ git show v1.0
tag v1.0
Tagger: chmartinez 
Date:   Wed Nov 7 9:05:33 2018 +0300

Release version 1.0
----------BEGIN PGP SIGNATURE-----
Version: GnuPG v1

iMTvhAA...
----------END PGP SIGNATURE-----

commit 7d44b6bb8abb96dee33f32610f56441496d77e8a
Author: chmartinez 
Date:   Wed Nov 7 9:05:33 2018 +0300

    Edited the Login form
...
```

It prints the author's name, creation date, message, GnuPG signature if present and the information about the referenced commit. If the tag is lightweight, the output will be limited to the information about the referenced commit.

**Editing tags** - `git tag -a -f <tag_identifier> <commit_id>`

If you try to create a tag with the same identifier as an existing tag, Git will throw an error: `fatal: tag 'v1.0' already exists.`

Instead of having to delete it and re-add the tag you can simply replace it while keeping the existing description. Choose the place in your commit history with `<commit_id>` where you want the tag moved to and add `-f` or `-force` to your command.

> Remember to alert your team members when you "force" a change like this. If they still have an "old" version of the tag, it may cause conflicts when they try to push to the server!

If you have already **pushed the tag** to the server and want to fix that, first make sure your local version of the tag is correct before you run the following command: `git push origin -f --tags.`

**Deleting tags** - `git tag -d <tag_identifier>`

Generally, there is no reason to **delete the tags** because they are inexpensive and don't use any resources unless you have mistakenly created a tag pointing to the wrong commit.

In case the tag has been already **pushed** and you need to remove it from remote repository run: 

```
$ git push origin :v1.0.
```

**Publishing tags** - `git push <location> <tag_identifier>`

A tag is just a reference to your local repository and it is _not_ automatically pushed to the remote repository with the rest of the code. Instead, you can `git push` the tag individually, or you can run `git push --tags` which will push all tags at once. It can be done similarly to pushing the branches:

```
$ git push origin v1.0
```

**Sorting tags** - `git tag --sort=<type>`

When looking at a project with lots of tags, using the [sort option](https://stackoverflow.com/questions/14273531/how-to-sort-git-tags-by-version-string-order-of-form-rc-x-y-z-w?#answer-22634649) can come in handy. Supported types are:

* `refname`(sorts in a lexicographic order),
* `version:refname` or `v:refname` (here tag names are treated as versions).

```
git tag -l --sort=-version:refname "v*"
```

Here I am listing all tags which name starts with "v" by their versions.

* * *