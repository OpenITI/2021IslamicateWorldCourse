# 2021IslamicateWorldCourse

This is the GitHub repository for the bookdown course website for the 2021 UMD and AKU course *The Islamicate World 2.0: Studying Islamic Cultures through Computational Textual Analysis*.

You can Access the course website here: https://openiti.github.io/2021IslamicateWorldCourse/

## Note for contributors: 

A very short and easy explanation of Bookdown can be found here: https://bookdown.org/home/about/

1. Clone the current repository on your local machine: 

`$ git clone https://github.com/OpenITI/2021IslamicateWorldCourse.git`

2. The course website consists of a number of pages - all files in the root directory of the repository with the extension `.Rmd`: 

```
index.Rmd
01-Week1.Rmd
02-Week2.Rmd
...
14-Week14.Rmd
```

Each of these files can be edited using RStudio

3. in RStudio, go to `File > Open Project`. This will open a file selection dialog; navigate to the repository you cloned, and select the `2021IslamicateWorldCourse.Rproj` in it

![Select Rproj](img/Rproj.png)

If the project file is not there, choose `File > New Project`, and select the repository you cloned.

4. In the bottom right corner, you will now see the contents of the project folder. Click one of the .Rmd files to edit it. 

5. Edit the file (use Pandoc markdown tags; full overview here: https://pandoc.org/MANUAL.html#pandocs-markdown)

6. When you want to visualize your changes, save (ctrl + s) and then click the "Knit" button in the tab of the document you are editing:

![knit](img/knit.png)

This will create a temporary build of the entire website and open a new window in R in which you can preview your changes. 

7. When you are finished with your work, save your changes (ctrl + s) and click the `Build` tab in the upper right section of RStudio:

![build](img/build.png)

8. In the `Build` tab, click the downward arrow next to the `Build Book` button, and choose `bookdown::gitbook`: 

![build gitbook](img/build_gitbook.png)

This will build the static html pages from your .Rmd files (they are stored in the `_books` folder in the repository).

9. Save your changes in Git: open Git Bash and use the following commands: 

```
$ git add .
$ git commit -m "Add new course details"
$ git push origin main
```

10. If you want to publish your changes to the public website: push your changes to the `gh-pages` branch, from which the website is served. This can be done using a shell script in Git Bash: 

`$  ./update_website.sh`

NB: The shell script will run this command: `git subtree push --prefix _book origin gh-pages`. For an explanation of this command, see https://dev.to/letsbsocial1/deploying-to-gh-pages-with-git-subtree

11. Your changes will be reflected on the live web page (this may take a couple of minutes): https://openiti.github.io/2021IslamicateWorldCourse/


# Tips and tricks

## Prerequisites for building the PDF version:

* download and install the MikTeX program from here: [https://miktex.org/download](https://miktex.org/download)

NB: make sure to choose the option that MikTeX is allowed to update/get new packages without asking, otherwise the PDF creation will fail

* in RStudio: run `install.packages("tinytex")`

## Pushing _books folder to gh-pages

The R script outputs the html, pdf and epub files into the _books folder.
Unfortunately, GitHub cannot serve html files that are not in the root folder of a repo. 
The solution is to create a gh-pages branch in the repo, to which only the _books folder is pushed. 

https://dev.to/letsbsocial1/deploying-to-gh-pages-with-git-subtree

Once the subtree and the gh-pages branch are set up, publishing changes in the files to be served is as easy as writing the following command in the `main` branch of the repo:

`$ git subtree push --prefix _book origin gh-pages`



### Initializing the gh-pages branch and the subtree:

**NB: this has to be done only once! Use the previously mentioned command for updating the gh-pages branch!**

1. create a local branch `gh-pages` and check it out: 

`$ git checkout -b gh-pages`

2. Make sure it is empty: 

`$ git rm -rf .`

(don't forget the `.` at the end!)

3. commit and add the removal of all hidden files:

`$ git commit -am "First commit to gh-pages branch"`

4. Push changes to remote `gh-pages` branch: 

`$ git push origin gh-pages`

5. Go back to the main branch: 

`$ git checkout main`

6. Create the subtree: 

```
git push origin `git subtree split --prefix _book gh-pages`:gh-pages --force
```

(note the backticks before "git subtree" and "_book gh-pages"!)
