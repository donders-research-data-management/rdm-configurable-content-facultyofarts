# Editing the configurable content of the Donders Repository portal

This page provides instructions for content manager to edit the configurable contents of the Donders Repository portal.

## How to edit

In the repository, you will see two branches, the _master_ and the _release_.  __You should only edit the master branch__.  Thus, before you start editing, make sure that you are on the master branch.

There are two ways of editing the static content:

1. edit directly on the GitHub web interface. Changes are committed right way to the repository.
1. edit on a local copy of the repository.

    Make a local copy of the repository:

    ```bash
    $ git clone https://github.com/donders-research-data-management/rdm-configurable-content-donders.git
    $ cd rdm-configurable-content-donders
    ```

    Edit the files with your favorite text editor.  With this method, changes need to be committed and pushed to GitHub by

    ```bash
    $ git commit -a -m 'message about the change'
    $ git push
    ```

## What to edit

The configurable content to be modified by the content manager are the following type of data:

- __Indices__ are files providing references or elaborated data for the portal to create human-friendly contents at various places in the portal.
- __Snippets__ are files providing part of the HTML body to be incorporated in various portal pages.
- __Styles__ are files used to provide customised style of the portal.

### Indices

The indices files are directly consumed by the portal code to create content dynamically.  Thus, they are presented in a machine-readable format, such as JSON and CSV, in the repository. Given the flexibility of the JSON format, indices in CSV formats are converted into JSON during the deployment process, using the [tools/csv2json.py](tools/csv2json.py) script.

A list of indices are given blow:

* [external_urls.json](external_urls.json) contains links to local contents (i.e. contents provides by this repository) or remote resources (i.e internet resources).  The local contents are specified with `/` followed by a path relative to the repository's directory; while the remote resources are specified with a URI protocol, such as `http://` or `https://`.

* [doc/dua/data_use_agreement.json](doc/dua/data_use_agreement.json) provides a list of Data Use Agreements, each has its `id`, `name`, and relative `path` to the content.  Note that the `path` is provided as a relative path as the content are provided locally from the repository.  This list is used by the portal to generate the DUA options on the collection editing form of the Data-Sharing Collections.  The order is respected.

* [doc/ethics/ethics_review_board.json](doc/ethics/ethics_review_board.json) provides a list of Ethical Review Boards, and they are grouped in different categories.  This list is used by the portal to generate the Ethical Review Board options on the collection editing form of the Data-Acquisition Collections.  The order is also respected.

* [doc/publication/publication_systems.json](doc/publication/publication_systems.json) provids a list of supported resource identifier systems that are used by the portal to generate the Publication System options on the collection editing form of the Data-Sharing Collections.  Each item on the list shoudl consists of the full name (`system`), the short name (`pidType`), and the URL prefix (`urlPrefix`).

* [doc/keyword/MeSH2015.csv](doc/keyword/MeSH2015.csv) and [doc/keyword/SFN2013.csv](doc/keyword/SFN2013.csv) are two controlled vocabularies currently supported by the Donders Repository for collection keywords.  They are provided in the CSV format, and will be converted to a JSON format during the deployment.  __For the moment, adding a new keyword set requires development works in the Donders Repository.__

As the JSON documents are imported by the portal code, invalid JSON document can cause errors.  Therefore, all the JSON indices come with a schema file for validating the JSON document during the build process. This process prevents broken JSON indices being deployed to the production system. __One should make sure the schema matches the modified JSON file so that the build process will not fail.__  

### Snippets

Snippets are HTML files that will be inserted in relevant portal pages, providing useful information to the portal users.  For a consistent look-n-feel on the portal, one should prevent any CSS-styling in the snippet.

Supported snippets are listed below:

* [doc/login.html](doc/login.html) contains text to be shown on the portal's login page, after the user clicks on the `LOG IN` button.

* [doc/logout.html](doc/logout.html) contains text to be shown on the portal after the user logs out the portal.

* [doc/signup.html](doc/signup.html) contains text to be shown on the portal after the user signed up to the portal the first time.

* [doc/homepage.html](doc/homepage.html) contains text to be shown on the portal's homepage.

* [doc/footer.html](doc/footer.html) contains text to be shown on the footer of every portal page.

* [doc/privacy_policy.html](doc/privacy_policy.html) contains the privacy policy of the Donders Repository.

* [doc/requestaccess.html](doc/requestaccess.html) contains text guiding user to request data access to a published collection.  The text is used, e.g., in the "Content" tab of the collection detail page.

* [doc/downloadcontent.html](doc/downloadcontent.html) contains text guiding user to download data via a data access method, such as WebDAV.

* [doc/email/collectionChangesLeadText.html](doc/email/collectionChangesLeadText.html) provides leading message of the notification email concerning recent collection changes.

* [doc/email/managerLessCollectionsLeadText.html](doc/email/managerLessCollectionsLeadText.html) provides leading message of the notification email concerning manager-less collections.

* [doc/dua/\*.html](doc/dua/RU-DI-HD-1.0.html) provides contents of a specific data use agreement.

### Styles

Currently, the CSS-style is coded in the portal code.  The only customisable components in style are logo and background.

* [doc/style/logo.png](doc/style/logo.png): A 100px height logo in png format (logo.png). Width can vary but the height is important to keep the aspect ratio.

* [doc/style/logo@2x.png](doc/style/logo@2x.png): A 200px height logo in png format for retina screens. Width can vary but the height is important to keep the aspect ratio.

## Providing online helps

Apart from configurable contents provided by this repository, there is also a mechanism in the portal to provide a online help.  By making use of the index file [external_urls.json](external_urls.json), this mechanism allows content manager to provide various help buttons in the portal links to their specific help documents.

### Finding available online help entries
