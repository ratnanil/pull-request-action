
```{.bash} 
# 1. render the unchanged project to latex
quarto render --to latex
# 2. Add and commit `_book` to the repo. 
# Note that this folder was in gitignore before.
git add -f _book
git commit -m "render original"
# get the pull request and merge with main
git fetch origin pull/$ID/head:new-pr 
git merge new-pr

# 3. render the changed project to latex
quarto render --to latex
# 4. Add and commit `_book` to the repo.
git add -f _book
git commit -m "render new"

# 5. run git-latexdiff


```

4. Render a changed project to tex (see step 1).
5. Run latexdiff filename_original.tex filename.tex > diff.tex. 
   - Note that the latex files are in a subfolder of the book folder, named after the title of the book. E.g. `_book_original/book-latex/testing.tex`
   - like I mentioned above, I'm not sure what happens with `_book_original` after checking out the pull request. If this folder still exists, the command would be as follows:
   ```
   latexdiff _book_original/book-latex/testing.tex _book/book-latex/testing.tex > diff.tex
   ```
   - This creates diff.tex in the root folder, which will probably not work with images etc. I probably want to create diff.tex in the new folder
6. Run pdflatex diff.tex diff.pdf. 
7. Attach this pdf as an artifact of the pull request.

