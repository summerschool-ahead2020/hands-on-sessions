# How to contribute

Thanks for your interest to contribute to this web page and your willingness to read this file.

## How this site works

The AHEAD2020 high-resolution spectroscopy school pages for the hands-on sessions are hosted
on Github and the source files are located in this repository. Each time a collaborator commits
changes to [this repository](https://github.com/summerschool-ahead2020/hands-on-sessions), Github
automatically converts the source file into HTML and publishes it
[here](https://summerschool-ahead2020.github.io/hands-on-sessions/index.html).

In order to be able to make changes to the website, you need a Github account and be included as
a member of the summerschool-ahead2020 organization. Please contact Liyi Gu or Jelle de Plaa for
more information.

## How to make changes

### Source file language

The source files of this website are written in [Restructured Text (.rst)](https://docutils.sourceforge.io/docs/user/rst/quickstart.html), which is a common format
used in source code documentation. These files are converted by Github into HTML using the
[Sphinx program](https://www.sphinx-doc.org/en/master/). See the links in this paragraph
for more information about the RST formatting syntax.

### Where to make changes?

The website source files are located in the ``doc`` directory in this repository. The
``index.rst`` file is the top-level page, and below that we have a directory for each
hands-on session of the workshop.

If you want to add instructions for, for example, the SNR session, then you can edit
the ``snr.rst`` file in the ``doc/snr/`` directory.

### How to make the changes?

#### Github web interface

The easiest is to use the Github web interface directly. You can click on the file that
you want to edit. Once the file opens, you can select ``edit file`` by clicking the pencil
icon in the top-right of the file window.

When you are in edit mode, you can make the necessary modifications. Once the edit is done,
you can click the green ``Commit changes`` button on the top-right to save them. You are asked
to provide a short description of the changes. For example: "Added instructions for the
SNR hands-on session" is a good short description.

After the file is saved, Github will re-build the website in a couple of minutes.
Please limit the number of commits, such that we do not overload Github with website build
requests.

#### Git clone

If you are familiar with git, you can also clone this repository, make
the changes locally, and commit and push them from your own computer.

### Can I convert my existing document to RST format?

If you have your instructions already in another format, then it is possible to convert
them to RST format. The most suitable program is [Pandoc](https://pandoc.org/MANUAL.html),
which is a Linux/Mac program to convert different types of formatted files to other formats.

Let us know if you have problems with using Pandoc. We can help converting your file
if necessary.

## Adding data files, notebooks, etc.

It is possible to host small data files on Github and create links to them in the
documentation. Simply upload the file (<100 Mb) to the directory of the session
(for example: ``doc/snr/``). In the snr.rst file, you can add a download link like this:
```
Please download :download:`spectrum.fits <spectrum.fits>` by clicking the link.
```

Please note that Github does not like to host files bigger than 50-100 Mb, so if you
want students to download large files, it is better to host them elsewhere. Then please
provide the link to the file on this site, instead of uploading it to this repository. In
RST a link can be made like this:
```
Please download the `NXB file <https://darts.jaxa.jp/pub/hitomi/data/nxb_20170510/ah_sxs_nxbafmar4_20140101v001.evt.gz>`_ by clicking the link.
```

## What if I have a problem?

Please contact Jelle de Plaa if you encounter issues with this system.