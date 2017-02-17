# What is this repo used for?

1. [healthcare.ai](http://healthcare.ai) main page (source and generated)
    - **Source** consists of
        - `.html` jekyll liquid templates in `jekyll/*`
        - markdown files in `jekyll/_posts`
        - lots of nice layouts (`jekyll/_layouts`) and includes(`jekyll/_includes`)
        - the jekyll config file (`jekyll/_posts`)
        - helper bash scripts to handle the jekyll build and directory shuffling
2. Py sphinx docs found at [healthcare.ai/py](http://healthcare.ai/py) (generated only)
    - **Source** files are in healthcare.ai-py repo in `docs` directory
    
## Notes

- All of these generated files are served via github pages on this repo from the root dir `/`, so there is by necessity
some unpleasant bash file manipulation.
- Building of R/Py docs is currently manual process and we use github pages from this repo.

## Compiling Bootstrap

1. Install grunt using the [bootstrap docs]((http://getbootstrap.com/getting-started/#grunt)).
2. Modify your .less files in `jekyll/public/bootstrap-3-3.7/less`
3. From the `jekyll/public/bootstrap-3-3.7/` directory, run `grunt dist` to compile the `.less` to `.css` (or if you're
making frequent changes run `grunt watch`)

## Updating the python package docs using sphinx

### Pre-requisites (only needed once)

- Clone the [healthcareai-py](https://github.com/HealthCatalystSLC/healthcareai-py) repo in addition to the
[documentation](https://github.com/HealthCatalystSLC/documentation) repo
- Install the packages with `pip install -r healthcareai-py/dev-requirements.txt`

### Update process

1. `cd` to the `docs` directory in the healthcareai-py repo
2. Edit the .rst files within docs folder
3. Build the docs and generate a `/py` directory via `sphinx-build -b html docs py`
4. Use `python -m http.server` to view the newly generated docs in `/py`
5. To place the docs within the right spot in the *documentation* repo, run `cp -rf py ../documentation`
6. Delete `/py` folder in the healthcareai-py repo via `rm -rf py`

## Creating a new blog post using Jekyll

This is the jekyll workflow until we use [readthedocs](https://readthedocs.org/) to build for us (hopefully soon)!

1. Add a new blog post source file in markdown format to `jekyll/_posts`
2. Run `jekyll build` from the `/jekyll` directory
3. Run `jekyll server` and check your post [locally in the browser](localhost:4000).

### QA the new post

1. From the repo root directory, run `./update_jekyll.sh`
    - This deletes all prior generated files to prevent cruft from building up.
2. From the repo root directory, run `python -m http.server` or `python -m SimpleHTTPServer` to see the entire site
 [served up locally](localhost:8000).
3. Verify all the things. Such as:
    - [localhost:8000/](localhost:8000/)
    - [localhost:8000/r](localhost:8000/r)
    - [localhost:8000/py](localhost:8000/py)
    - [localhost:8000/blog](localhost:8000/blog)
    - [localhost:8000/contact.html](localhost:8000/contact.html)
    - [localhost:8000/learn_more](localhost:8000/learn_more)
4. At this point it is suggested to use a perceptual diff tool like [dpxdt](https://dpxdt-test.appspot.com) to aid in
the QA process.

### Deploy the new post

1. After verifying the new post, deploy it to healthcare.ai
2. Commit changes to your branch.
3. Open a pull request.
4. Optionally have someone check your PR and do the merge in to master.
5. Check the [real website](http://healthcare.ai)
