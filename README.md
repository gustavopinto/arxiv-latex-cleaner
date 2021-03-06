This tool allows you to easily clean the LaTeX code of your paper to submit to
arXiv. From a folder containing all your code, e.g. `/path/to/latex/`, it
creates a new folder `/path/to/latex_arXiv/`, that is ready to ZIP and upload to
arXiv.

## Example call:

```
python -m arxiv-latex-cleaner.arxiv_latex_cleaner /path/to/latex/ --im_size 500 --images_whitelist='{"images/im.png":2000}'
```

## Main features:

#### Privacy-oriented

*   Removes all auxiliary files (`.aux`, `.log`, `.out`, etc.).
*   Removes all comments from your code (yes, those are visible on arXiv and you
    do not want them to be). These also include `\begin{comment}\end{comment}`
    environments.
*   Optionally removes user-defined commands entered with `commands_to_delete`
    (such as `\todo{}` that you at the end redefine as the empty string).

#### Size-oriented

There is a 10MB limit on arXiv submissions, so to make it fit:

*   Removes all unused `.tex` files (those that are not in the root and not
    included in any other `.tex` file).
*   Removes all unused images that take up space (those that are not actually
    included in any used `.tex` file).
*   Resizes all images to `im_size` pixels, to reduce the size of the
    submission. You can whitelist some images to skip the global size using
    `images_whitelist`.
*   Optionally compresses `.pdf` files using ghostscript (Linux and Mac only).

## Usage:

```
arxiv_latex_cleaner.py [-h] [--im_size IM_SIZE]
                       [--images_whitelist IMAGES_WHITELIST]
                       input_folder

positional arguments:
  input_folder          Input folder containing the LaTeX code.

optional arguments:
  -h, --help            show this help message and exit
  --im_size IM_SIZE     Size of the output images (in pixels, longest side).
                        Fine tune this to get as close to 10MB as possible.
  --images_whitelist IMAGES_WHITELIST
                        Images that won't be resized to the default
                        resolution, but the one provided here in a dictionary
                        as follows '{"path/to/im.jpg": 1000}'
  --compress_pdf        Compress PDF images using ghostscript (Linux and Mac
                        only).
  --commands_to_delete COMMANDS_TO_DELETE [COMMANDS_TO_DELETE ...]
                        LaTeX commands that will be deleted. Useful for e.g.
                        user-defined \todo commands.

```

## Note

This is not an officially supported Google product.
