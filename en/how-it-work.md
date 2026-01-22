# Main scenarios for Diplodoc usage
## Simple documentation project with YFM


### Project Structure
Basic project contains few config files and pages with actual content. Both config files and markdown linked into the following structure:


```
input-folder
|-- .yfm (config file for whole project)
|-- toc.yaml (table of content)
|-- presets.yaml (presets for vairables)
|-- index.yaml (index page)
|-- pages (Content pages)
    |-- faq.md
    |-- how-to.md
|-- _assets (directory with pictures)
    |-- image1.png
    |-- image2.png
|-- _includes (directory for reusable content)
    |-- faq_shared_block.md
```


More information about the structure can be found on [the page](./project/index.md). 



### Project Build
Build can be performed with "Builder" tool with cli. 

For build initiation run the following with **mandatory** keys:

-  input, -i — path to project directory.


- output, -o —path to directory with output data (static HTML pages)


#### Example
```
yfm -i ./input-folder -o ./output-folder
```


### Result
After successful build you get either HTML-linked project or YFM.
YFM can be used for subsection creation. 


### Usage
HTML-linked and ready project can be used locally, hosted on your favorite provider or placed into S3-like storage for further processing. 



## Integration into Development pipeline
### Project creation and build

For common scenarios project structure and build procedures are the same as mentioned in previous section.
But in case of integration with your CI/CD pipelines it's required to include Builder for triggers on documentation updates in repository.



### Plugins and extended configuration 
Huge documentation projects are using extra capabilities for content processing and specific configurations for build. As an example - you can use plugins for complex tables of work with video. More details can be found on [the page](./plugins/index.md).



## Work with GitHub and publication on your own domain or on https://diplodoc.com 

If you are using GitHub as your VCS and repository for your documentation - Diplodoc can be used for full pipeline creation, starting from making changes in .md files to hosting pf your project.

[Contact us](https://diplodoc.com/#contact), to discuss details of your configuration.