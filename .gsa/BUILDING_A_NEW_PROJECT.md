# Building a new project

This base repo collects common code and information shared between all projects. To use it, you need to build a specific one. To do that, first create a new repository and clone it to your own machine. There isn't a README.md file in this repository, so you can add that to the project repo, but you should not add a .gitignore, as that should come from the build-specific mixin.

In the new project repo, we need to setup a remote pointer to this base repo.

```sh
> git remote add base https://github.com/birc-gsa/gsa-project-base
> git fetch base
> git merge base/main --allow-unrelated-histories
```

Now you have a connection to the base-repo so you can fetch and merge updates in the future. Any time you need to pull down changes from the base repo, repeat

```sh
> git fetch base
> git merge base/main
```

In the new project, you can describe the specific project; use README.md for that, and you can configure the testing setup specific to the project. As a minimum, you need to add `.gsa/test-test.yml`. It is currently empty, but it must be populated for the testing workflow to function. An example could be this:

```yaml
tools:
  TM-Naive:
    map: "gsa search {genome} {reads} -o {outfile} exact naive"
  TM-Border:
    map: "gsa search {genome} {reads} -o {outfile} exact border"
  search:
    map: "{root}/search {genome} {reads} > {outfile}"
  
reference-tool: TM-Naive

genomes:
  length: [100, 500, 1000]
  chromosomes: 10

reads:
  number: 10
  length: [10, 50]
  edits: 0
```
