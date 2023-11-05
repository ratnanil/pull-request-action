

1. render the unchanged project to latex:
    ```
    quarto render --to latex
    ```
2. Make a copy of this project (is this necessary? Maybe I can just commit the changes to the branch and compare the branches afterward?)
   ```
   cp -r _book _book_original
   ```
3. Check out the pull request. 
   - Locally, I would need to know the pull request number. On the gh-action, there is a variable for this.
   - Will `_book_original` still exist after checkout?
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

