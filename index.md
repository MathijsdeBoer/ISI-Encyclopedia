This repository aims to provide an overview of concepts and topics that can help you start working with the resources provided in the Image Sciences Institute (ISI) faster. The files have been written in [Obsidian.md](https://obsidian.md/), which is a note taking app that allows for crosslinking between your notes. A benefit of this application is that its files are in the universal [Markdown](https://daringfireball.net/projects/markdown/) (`.md`) format, which is supported by many rendering and parsing engines across the internet. However, crosslinking may not work properly, so you might see some terms with
```markdown
[[brackets]]
```
around them if you read the raw `.md` files on GitHub, or any other place you might find this.

Future endeavors include an HTML export of the notes on a regular basis, so that these crosslinks are properly handled.
# Editing
The source files that are used to generate this project are currently found [here](https://github.com/MathijsdeBoer/ISI-Encyclopedia). To edit the files you can simply open them in your text editor of choice. However, it is recommended that you install Obsidian if you want to do more extensive editing.
# Deploying
We use the [Webpage HTML Export Plugin](https://github.com/KosmosisDire/obsidian-webpage-export) to generate the HTML pages for the website. Any new exports should be placed in the `docs` directory for an automatic redeployment. To preserve some processing power (and perhaps some money) deployments should be limited to every once in a while.