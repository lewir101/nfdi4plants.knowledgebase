---
layout: docs
title: Knowledge base contribution guide
published: 2022-07-08
author_github: brilator
add toc: false
add sidebar: _sidebars/mainSidebar.md
article_status: published
todo:  
  - commenting in documents
---

Your contribution to the DataPLANT knowledge base is highly appreciated.
This guide is intended to show you how to contribute new articles and tutorials or review and adapt parts of existing ones.
<!-- most efficiently for you and the knowledge base curators -->

<!-- TODO check link!! -->
For smaller changes and suggestions, please refer to https://nfdi4plants.org/nfdi4plants.knowledgebase/content/docs/index.html.


- [Introduction](#introduction)
- [GitHub Routines](#github-routines)
- [Testing](#testing)
- [Common errors](#common-errors)
- [Docs-Page](#docs-page)
- [_sidebar](#_sidebar)
- [Markdown to HTML Rendering Rules](#markdown-to-html-rendering-rules)
  - [Ignored Content](#ignored-content)
  - [Visible or Hidden](#visible-or-hidden)
- [References](#references)
- [Structure and Format](#structure-and-format)
- [Images](#images)
- [File Name Requirements](#file-name-requirements)
- [Addressing Readers](#addressing-readers)
- [Language](#language)


## Introduction

The DataPLANT knowledge base is built on [nfdi-web-components](https://nfdi4plants.github.io/web-components-docs/) and will fit all **markdown** content into this "framework".
For a general introduction to writing markdown, see: [Markdown tutorial](tutorials/markdown.md) and references therein.

## GitHub Routines

> Note: This is not a full-fledged GitHub tutorial. Please refer to available tutorials online or contact the knowledge base curators.

1. Sign up for a GitHub account.
2. [Fork](https://github.com/nfdi4plants/nfdi4plants.github.io/fork) the knowledge base git repository.
   
   - This creates a copy of the knowledge base repository in your own GitHub account.
   - In the top left, you will see that the repository is associated with your account (1) and forked from the main repository (2).
   - You can either directly add or edit content using GitHub or clone (3) your repository to work on it locally.
   - Be aware that your fork is not automatically updated, if the main repository updates. Make sure to update your fork regularly (especially before creating new content) by clicking "Fetch upstream" (4) in the top-right corner of your repository.
   - If you cloned your repository locally, you also have to update the local clone (via "git pull").
   
  ![Git Routine](./img/contribution_git.png)

3. You can work and make any changes in your own repository and commit + push them to your fork.

4. Once you want to submit those changes to the main repository, you can open a "pull request" by clicking "Contribute" (5) in the top-right corner.
   > Remember to "Fetch upstream" (4), if your fork is not up-to-date with the main repository.

5. If edited or added existing content, please assign the original author during your pull-request to review your changes.
  
  - The github user name of the original author is stored in the yaml block on top under `author_github`
  - During the pull-request mention the author via `@<author_github>`.

## Testing

Check out the README.md in the [root directory](../../README.md) for instructions on how to install the knowledge base locally on your machine.
Following those instructions allows you to test and see how your changes come into play and wether everything renders correctly.

It's highly recommended to *frequently* check your changes locally.
Please **do not** produce and submit a lot of content without prior local testing.

## Common errors

- Missing metadata block
- Missing or false required (`MUST`) attribute in metadata block
- Using a layout in metadata block that does not exist
- Wrong links
  - to sidebar elements
  - to images

# Authoring content

## Docs-Page

To add more documentation, add a markdown file to `/src/docs`. The file MUST start with a metadata block:

<!--used yml here as code language for nice color syntax-->
```yml
---
layout: docs
title: Metadata
published: 2022-05-09
author: Dominik Brilhaus
author_orcid: https://orcid.org/0000-0001-9021-3197
author_github: brilator
add toc: true
add sidebar: _sidebars/mainSidebar.md
article_status: published
todo:
    - update to include changes in latest tool version
---
```

- All keys (`layout`, `author`, etc.) are **not** case sensitive.
- All fields can be at ANY position.
- MUST start and end with `---` .
- MUST contain `layout: docs`.
  - This triggers fornax parsing to html.
- MUST contain `title: xxxx`.
  - Will be added as "# xxxx" to the html.
  - Will be used to name the generated webpage.
- MUST contain `published: yyyy-MM-dd`.
- MAY contain `author: xxxx`.
- MAY contain `author_github: xxxx`.
  - This helps authoring and reviewing content. 
- MAY contain `add toc: true`.
  - Will add automated table of contents from all found headers in content.
- MAY contain `add sidebar: realtive\path\to\sidebar.md` to add the sidebar element to the page.
- MAY contain **any** other metadata. The information will be read but will not affect the generated html.

## _sidebar

Sidebar files MUST be in any **subdirectory** of `/src/docs/_sidebars`. Sidebar markdown files must start with a metadata block:

```yml
---
published: 2022-05-09
article_status: published
---
```

- MAY contain **any** other metadata. The information will be read but will not affect the generated html.

To add a sidebar element to the page, use the codeblock syntax:

<pre><code>```Data Management Plan
# Data Management Plan:/docs/DataManagementPlan.html
# DataPLANT's Data Management Plan Generator:/docs/DataManagementPlan.html#dataplants-data-management-plan-generator
```</code></pre>

- All text after the opening "```" will be parsed to the element title.
- Inner text MUST only contain heading lines.
  - Only headers up to `###` are parsed. All header with more depth are parsed to `###`.
- Tries to match active browser url to referenced ``href`` of any element to set active page.

## Markdown to HTML Rendering Rules

Every markdown document stored in `/nfdi4plants.knowledgebase/src/docs` or any subfolder (except `_ignored`) will be rendered to html and become publicly available once pushed to the main repository.

### Ignored Content

- Anything inside the folder `_ignored` will not be used to generate html pages.
- This folder is intended for ideas and drafts that
  - should not yet become available in the knowledge base
  - should be under version control for discussion and reviewing

### Visible or Hidden

Although most markdown content will be rendered and published, it will not prominently be visible to all visitors.
It will only become visible in the sidebar once the article is linked in the respective sidebar (typically `add sidebar: _sidebars/mainSidebar.md`)

# Content Design Principles

## References

- Literature / information references: additional bibliography block below
- External links (tools, sites, platforms): as hyper-link
- Knowledge base cross-references: relative path to *.md document, **BUT** replace the `.md` file extension with `.html`, as the markdown files are parsed to html.

## Structure and Format

Try to avoid deep structures by using no more than two headline levels, i.e.

<pre><code>```
## Headline level 2 <!-- omit in toc -->
### Headline level 3 <!-- omit in toc -->
```</code></pre>

Level 1 is automatically generated from the article's `title: `.

## Images

- simple markdown logic (not HTML): `![name_of_image](path_to_image.png)`

## File Name Requirements

File names:

- MUST use the article's title for the filename, e.g.: DataManagementPlan.md -> `title: Data Management Plan`
- MUST NOT contain special characters
- MUST NOT contain spaces
- MUST use [snake_case](https://en.wikipedia.org/wiki/Snake_case) (lower_case_with_underscores) OR [PascalCase](https://techterms.com/definition/pascalcase) (UpperCase)

> Remember: Changing file names (and paths) means changing URLs and can easily lead to dead links.

## Addressing Readers

We generally try to address users and readers directly.
Use "you can", not "the user can" or "one can..."

## Language

British English

> Note: If you work with Visual Studio Code -
> Check out the extension "Code Spell Checker" https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker
> with British English ("cSpell.language": "en-GB") support.

# Link Collection

> Note: This is just a link collection for recurrent use in KB articles
> Nothing automatised. Just copy/paste.

⚠️ Must be read from markdown, will not be shown in html.

<!-- Links to DataPLANT knowledge base (kb-) -->

[kb-AnnotatedResearchContext]: ./AnnotatedResearchContext.html "Annotated Research Context"
[kb-DataHub]: ./DataHub.html "DataPLANT DataHUB"
[kb-DataManagementPlan]: ./DataManagementPlan.html "Data Management Plan"
[kb-DataPublications]: ./DataPublications.html "Data Publication"
[kb-DataSharing]: ./DataSharing.html "Data Sharing"
[kb-FairDataPrinciples]: ./FairDataPrinciples.html "FAIR Data principles"
[kb-Metadata]: ./Metadata.html "Metadata"
[kb-PersistentIdentifiers]: ./PersistentIdentifiers.html "Persistent Identifiers"
[kb-PublicDataRepositories]: ./PublicDataRepositories.html "Repositories"
[kb-QuickStart_arc]: ./QuickStart_arc.html "Quickstart ARC"
[kb-ResearchDataManagement]: ./ResearchDataManagement.html "Research Data Management"
[kb-VersionControlGit]: ./VersionControlGit.html "Git"

<!-- Links to DataPLANT Homepage (hp-) -->

[hp-Registration]: <https://register.nfdi4plants.org/registration> "DataPLANT Registration"
[hp-DataHUB]: <https://git.nfdi4plants.org> "DataPLANT DataHUB"
[hp-HelpDesk]: <https://helpdesk.nfdi4plants.org> "DataPLANT Help Desk"

<!-- Links to DataPLANT GitHub (gh-) -->

[gh-ArcSpecs]: <https://github.com/nfdi4plants/ARC-specification/> "ARC specifications"
[gh-ArcCommander]: <https://github.com/nfdi4plants/arcCommander/wiki> "ArcCommander Wiki"
[gh-Swate]: <https://github.com/nfdi4plants/Swate/wiki> "Swate Wiki"

<!-- Links to external (ext-) sources -->

[ext-galaxy]: <https://plants.usegalaxy.eu/> "Galaxy Plants"
[ext-omero]: <https://www.openmicroscopy.org/omero/> "Omero"
[ext-zenodo]: <https://zenodo.org/> "Zenodo"
[ext-invenio]: <https://inveniosoftware.org/products/rdm/> "Invenio"
[ext-DataJournals]: https://www.researchdata.uni-jena.de/en/information/data-publication "RDM Jena Data Journals"

[ext-EBI-PRIDE]: https://www.ebi.ac.uk/pride/ "EBI PRIDE"
[ext-re3data]: https://www.re3data.org/ "re3data.org"
[ext-CreativeCommons]: https://creativecommons.org/ "Creative Commons"
[ext-DublinCore]: <https://www.dublincore.org/specifications/dublin-core/dcmi-terms/> "DublinCore"
[ext-DataCite]: <https://schema.datacite.org>  "DataCite"
[fairsharing.org]: https://fairsharing.org/search?fairsharingRegistry=Standard "Standards at fairsharing.org"
[doi]: https://www.doi.org/ "Digital Object Identifier"
[orcid]: https://www.orcid.org/ "ORCID"