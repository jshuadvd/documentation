# What is this repo used for?

1. [healthcare.ai](http://healthcare.ai) main page (source and generated)
    - **Source** consists of raw .html pages and markdown in `jekyll/_posts`
2. R documentation (source and generated) generated by mkdocs found at [healthcare.ai/r](http://healthcare.ai/r)
    - **Source** files are in this repo in `templates` directory
3. Py sphinx docs found at [healthcare.ai/py](http://healthcare.ai/py) (generated only)
    - **Source** files are in healthcare.ai-py repo in `docs` directory
    
## Notes

- All of these generated files are served from github pages on this repo, so there is by necessity some redundancy and
obscure folder structure.
- Building of R/Py docs is currently manual process and we use github pages from this repo.
- Please do a pull request if you see typos!

## Compiling Bootstrap

1. Install grunt using the [bootstrap docs]((http://getbootstrap.com/getting-started/#grunt)).
2. Modify your .less files in `public/bootstrap-3-3.7/less`
3. From the `public/bootstrap-3-3.7/` directory, run `grunt dist` to compile the `.less` to `.css` (or if you're making
frequent changes run `grunt watch`)

## Updating R package docs with mkdocs

1. `cd` to root directory of repo
2. Edit .md ([Markdown](https://daringfireball.net/projects/markdown/syntax)) files in the `/templates` folder
3. Run `mkdocs build` to generate new docs in the `/r` directory
4. Run `mkdocs serve` or `python -m http.server` to view docs

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
2. Run `jekyll build` from the jekyll directory
3. Run `jekyll server` and check your post [locally in the browser](localhost:4000).

### QA the new post

1. In the top-level repo directory, run `./update_jekyll.sh`
2. Run `python -m http.server` to  [locally in the browser](localhost:8000) via  Note: now use port :8000
3. Verify that things like good not only on healthcare.ai/blog, but also /py and /r

### Deploy the new post

1. After verifying the new post, deploy it to healthcare.ai
2. Commit, push, and check the real website.
