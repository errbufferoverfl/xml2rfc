# xml2rfc, a markdown fork


<div align="center">

##### A hacky fork of xml2rfc that adds Obsidian-Markdown support for RFCs and IETF drafts from document source in XML according to the IETF xml2rfc v2 and v3 vocabularies

</div>

[![This project is considered experimental](https://img.shields.io/badge/Status-experimental-red.svg)](https://www.arp242.net/status/experimental)

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
  - [Getting Started](#getting-started)
  - [Docker Dev Environment](#docker-dev-environment)
- [Maintenance Policy](#maintenance-policy)

---

## Introduction

The [IETF] uses a specific format for the standards and other documents it publishes as [RFCs], and for the draft 
documents which are produced when developing documents for publications. There exists a number of different tools to 
facilitate the formatting of drafts and RFCs according to the existing rules, and this tool, **xml2rfc**, is one of 
them. It takes as input an xml file that contains the text and meta-information about author names etc., and transforms 
it into suitably formatted output. The input xml file should follow the grammars in [RFC7749] *(for v2 documents)* or 
[RFC7991] *(for v3 documents)*. Note that the grammar for v3 is still being refined, and changes will eventually be 
captured in the [bis draft for 7991]. Changes not yet captured can be seen in the xml2rfc source [v3.rng], or in 
the [documentation xml2rfc produces] with its `--doc` flag.

**xml2rfc** provides a variety of output formats. See the command line help for a full list of formats. It also 
provides conversion from v2 to v3, and can run the [preptool] on its input.

## Usage

**xml2rfc** accepts multiple XML documents as input and outputs to one or more conversion formats.

### Basic Usage

```sh
xml2rfc SOURCE [options] FORMATS...
```

Run `xml2rfc --help` for a full listing of command-line options.

### Getting Started

Because this iteration is super hacky there are a few quirks that you probably wouldn't see in the original xml2rfc 
-- but that version doesn't have markdown support does it! So you'll tolerate it!

The markdown generator works best on unprocessed files, so if you've downloaded one of the bulk archives I'd 
recommend running the un-prepper first:

```sh
xml2rfc --unprep
```

I've built in some hacky bulk processing so once you have your unprepped files put all of them into a new directory 
that only contains the unprocessed XML. Then you can run:

```sh
xml2rfc ../DIRECTORY/ --markdown
```

Flags like `--path` are still operational which means you can export all your processed files to a different 
directory, but I would err caution in using this version to process files into the officially supported formats.

Most of the changes have been annotated with `# NOTE (errbufferoverfl)` so you can take a look at how and where 
changes have been made, but some bug whacking has been done and there may be undocumented changes.

### Docker Dev Environment

Run `./run.sh` command to build and start a docker development environment.
The initial build may take time because it downloads all required fonts as well.

```sh
./run.sh
```

## Maintenance Policy

This fork of xml2rfc was developed for my own use cases and is completely experimental. If you use this code and 
find issues you are welcome to raise a ticket, however, there is no guarantee on the release of subsequent versions 
or bug fixes.

[IETF]: https://www.ietf.org/
[RFCs]: https://www.rfc-editor.org/
[RFC7749]: https://www.rfc-editor.org/info/rfc7749
[RFC7991]: https://www.rfc-editor.org/info/rfc7991
[bis draft for 7991]: https://datatracker.ietf.org/doc/draft-iab-rfc7991bis/
[v3.rng]: xml2rfc/data/v3.rng
[documentation xml2rfc produces]: https://ietf-tools.github.io/xml2rfc/
[preptool]: https://www.rfc-editor.org/info/rfc7998
[WeasyPrint]: https://weasyprint.org/
[WeasyPrint Docs]: https://doc.courtbouillon.org/weasyprint/stable/first_steps.html
