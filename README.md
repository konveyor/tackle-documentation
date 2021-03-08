<img src="assets/img/konveyor-logo-tackle.svg" alt="Logo" width="100" />

# Tackle documentation

Tackle is an upstream project for refactoring applications for Kubernetes.

## Contributing to Tackle documentation

Read the [Guidelines for Red Hat Documentation](https://redhat-documentation.github.io/) before opening a pull request.

### Upstream and downstream variables

This document uses the following variables to ensure that upstream and downstream product names and versions are rendered correctly.

| Variable | Upstream value | Downstream value |
| -------- | -------------- | ---------------- |
| project-full | Tackle | MTA Pathfinder |
| project-short | Tackle | MTA Pathfinder |
| project-version | 1.0 | 1.0 |

Variables cannot be used in CLI commands or code blocks unless you include the "attributes" keyword:

	[options="nowrap" subs="+quotes,+attributes"]
	----
	# ls {VariableName}
	----

You can hide or show specific blocks, paragraphs, warnings or chapters with the `build` variable. Its value can be set to "downstream" or "upstream":

	ifeval::["build" == "upstream"]
	This content is only relevant for Tackle.
	endif::[]

### Building a document preview

You can build a document preview by running a Jekyll container.

You must have Podman installed.

1. Clone the repository:
  ```console
  $ git clone -b source https://github.com/konveyor/forklift-documentation.git && cd forklift-documentation
  ```
2. Create `.jekyll-cache` and `_site` directories:
  ```console
  $ for i in .jekyll-cache _site; do mkdir ${i} && chmod 777 ${i}; done
  ```
3. Create a `Gemfile.lock` file:
  ```console
  $ for i in Gemfile.lock; do touch ${i} && chmod 777 ${i}; done
  ```
4. Run a Jekyll container:
- If your operating system is SELinux-enabled:

  ```console
  $ podman run -it --rm --name jekyll -p 4000:4000 -v $(pwd):/srv/jekyll:Z jekyll/jekyll jekyll serve --watch --future
  ```

  **Note**: The `Z` at the end of the volume (`-v`) relabels the contents so that they can be written from within the container, like running `chcon -Rt svirt_sandbox_file_t -l s0:c1,c2` yourself. You must run this command in the cloned directory.

- If your operating system is not SELinux-enabled:

  ```console
  $ podman run -it --rm --name jekyll -p 4000:4000 -v $(pwd):/srv/jekyll jekyll/jekyll jekyll serve --watch --future
  ```

5. Navigate to `http://<localhost>:4000` in a web browser to view the preview.
