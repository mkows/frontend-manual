HBC Accessibility Guideline
=====

- [1. Objective](#1-objective)
- [2. ADA](#2-ada)
- [3. Accessibility standard - WCAG 2.0](#3-accessibility-standard---wcag-20)
- [4. ARIA](#4-aria)
  - [4.1. Role](#41-role)
  - [4.2. Most useful ARIA attributes](#42-most-useful-aria-attributes)
- [5. Pa11y](#5-pa11y)
  - [5.1. Install](#51-install)
  - [5.2. How to use](#52-how-to-use)
- [6. ADA Reporter](#6-ada-reporter)
  - [6.1. Reporter script](#61-reporter-script)
  - [6.2. Google Exporter](#62-google-exporter)
  - [6.3. Dashboard](#63-dashboard)
  - [6.4. Roadmap/TODO](#64-roadmaptodo)
- [7. Functional Accessibility Tests](#7-functional-accessibility-tests)
- [8. Accessibility Pipeline](#8-accessibility-pipeline)
- [9. Screen Readers](#9-screen-readers)
  - [9.1. Voice Over](#91-voice-over)
  - [9.2. NVDA](#92-nvda)
- [10. Most found issues and how to fix them](#10-most-found-issues-and-how-to-fix-them)
  - [10.1. Alt text](#101-alt-text)
  - [10.2. Duplicate ids](#102-duplicate-ids)
  - [10.3. Links without href](#103-links-without-href)
  - [10.4. Labels](#104-labels)
  - [10.5. Modals](#105-modals)


# 1. Objective

The purpose of this document is to be a quick and practical reference on how to apply accessibility in the context of HBC projects. This document will not detail accessibility or explain the techniques, but give an overview of what has already been done to meeting the requirements of the ADA, what needs to be maintained, and what still needs to be done.

There are great articles and resources about accessibility in [WebAim](https://webaim.org/). We also indicate this free course on Udacity: [Web Accessibility](https://udacity.com/course/web-accessibility--ud891).


# 2. ADA

The [Americans with Disabilities Act](https://www.ada.gov/index.html) (**ADA**) is a civil rights law that prohibits discrimination against individuals with disabilities. Despite being the focus of this document, the law is not just about accessibility on the internet, but any areas of public life, including jobs, transportation, and places that are open to the general public.

The ADA is divided into five titles (or sections) that relate to different areas of public life. Although the language of the ADA does not explicitly mention the Internet, the Department has taken the position that title II covers Internet Web site access.

There is a [ADA Best Practices Tool Kit for State and Local Governments](https://www.ada.gov/pcatoolkit/chap5chklist.htm) with a website accessibility checklist.

Additional guidance is available in the Web Content Accessibility Guidelines (WCAG).


# 3. Accessibility standard - WCAG 2.0

[Web Content Accessibility Guidelines](https://www.w3.org/WAI/intro/wcag.php) (**WCAG**) has the goal of providing a single shared standard for web content accessibility that meets the needs of individuals, organizations, and governments internationally. It is developed and maintained by the [Web Accessibility Initiative](https://www.w3.org/WAI/) (**WAI**), is a subgroup of the World Wide Web Consortium (W3C).

The WCAG 2.0 has 12 guidelines that are organized under 4 principles: perceivable, operable, understandable, and robust. For each guideline, there are testable success criteria, which are at three levels: A, AA, and AAA.

![WCAG Standard][img-wcag-standard]

In order to be ADA compliant, we adopted the **WCAG 2.0 AA** standard.

# 4. ARIA

[Accessible Rich Internet Applications](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) (ARIA) defines ways to make Web content and Web applications (especially those developed with Ajax and JavaScript) more accessible to people with disabilities.

This specification provides an ontology of roles, states, and properties that define accessible user interface elements and can be used to improve the accessibility and interoperability of web content and applications.

## 4.1. Role

The `role` attribute defines the type of element. There are a lot of values that can be used, such as dialog, button, checkbox, progressbar, etc. See a list of roles in [Mozilla Aria Techniques](https://developer.mozilla.org/pt-BR/docs/Web/Accessibility/ARIA/ARIA_Techniques).

Web developers **must not** use the ARIA role and aria-* attributes in a manner that conflicts with the semantics described in the [Document conformance requirements for use of ARIA attributes in HTML](https://www.w3.org/TR/html-aria/#docconformance) table.

## 4.2. Most useful ARIA attributes

- aria-hidden

The `aria-hidden="true"` property turns a html element hidden/ignored by screen readers. This is very useful in decorative elements, such as a decorative icon inside a text block or title.

- aria-label / aria-labelledby

This attributes are used to tell screen reader which text should be read in a element. The difference is that aria-label receives directly the text, and aria-labelledby receives the elements IDs that should be used for screen reader.

- aria-live

Areas or widgets with dynamic content which updates without a page reload can be decorated with `aria-live="polite"`. The screen reader will speak changes in these areas whenever the user is idle. [See more about aria-live](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions).

See more about WAI-ARIA on [W3C Using ARIA](https://w3c.github.io/using-aria/).


# 5. Pa11y

[Pa11y](http://pa11y.org/) is a automated accessibility testing tool. It runs HTML CodeSniffer from the command line for programmatic accessibility reporting.

[CodeSniffer](http://squizlabs.github.io/HTML_CodeSniffer/) is a client-side script that checks HTML source code and detects violations of a defined coding standard. In our case, we run with WCAG 2.0 AA standard.

The report returns a lot of issues classified between Errors, Warnings or Notices. Anything that is not marked as an Error should be manually tested:
- Warnings are items that HTML_CodeSniffer are able to detect as a potential problem, but require manual inspection to determine whether it is a failure.
- Notices are items that HTML_CodeSniffer cannot automatically detect, but should be manually inspected to ensure compliance with the standard.

There are a lot of techniques that can be applied depending on the failed success criterion. See the complete [list of success criterion and techniques here](http://squizlabs.github.io/HTML_CodeSniffer/Standards/WCAG2/).

## 5.1. Install

Install Pa11y globally with [this npm package](https://www.npmjs.com/package/pa11y):

`npm install -g pa11y@beta`

We used pa11y version 5.x (currently beta version) in order to be able to use Chromium - pa11y 4.x uses phantomjs.

## 5.2. How to use

Run an accessibility test against a URL:

`pa11y http://example.com`

Or, in JavaScript:

```
const pa11y = require('pa11y');

pa11y('http://example.com/').then((results) => {
    // Do something with the results
});
```

See more in the [README on Pa11y github page](https://github.com/pa11y/pa11y/).


# 6. ADA Reporter

The ADA Reporter is a NPM Package that uses Pa11y to analyzes several pages on the common platform banners (Saks, Saks Off 5th and Lord & Taylor) and generate a report with the accessibility results.

All the necessary documentation to install and run can be found in [this repository on Github](https://github.com/saksdirect/ada-reporter).


## 6.1. Reporter script

The core command-line `ada-reporter` generates a report with the code errors found by banner and page in a JSON file. This generated report is used in Google Exporter, Dashboard and in the Pipeline.

See the options running `ada-reporter --help`

## 6.2. Google Exporter

Is possible to send the generated report to a Google Spreadsheet running the following command from project folder:

```
node google.js
```

## 6.3. Dashboard

There is an accessibility dashboard to display the report results available on the `./reports` directory. Start the express server running:
```
node dashboard.js
```

![Accessibility Dashboard][img-dashboard]


## 6.4. Roadmap/TODO

There are a lot of things to do:
- Split ADA Reporter project in different repositories by functionality;
- Allow to set Google Spreadsheet ID on the google.js script;
- Run pa11y actions from ada-reporter script (currently the actions are in another branch);


# 7. Functional Accessibility Tests

The main purpose of this test is to validate the execution of the purchase flow by a visually impaired user, having all navigation and interaction via a keyboard.

**Structure (Page objects + FluentLenium)**

The tests are in the structure of Smoke tests and can be found in the `saks_website` repository.

Run via command line:
```
./gradlew smokeTestSaksAccessibility -Dwebsite=<url_environment>
```


# 8. Accessibility Pipeline

The accessibility pipeline can be found on [GoCD](http://go.saksdirect.com/go/tab/pipeline/history/website-accessibility-check). This pipeline is triggered by the STQA deployment pipelines, which are  [Saks_QA_Website_Master](http://go.saksdirect.com/go/tab/pipeline/history/Saks_QA_Website_Master) -- deployment to Saks STQA from the _saks_website_ master branch -- and [Saks_QA_Website_Release](http://go.saksdirect.com/go/tab/pipeline/history/Saks_QA_Website_Release) -- deployment to Saks STQA from the _saks_website_ release branch.

![Accessibility Pipeline flow][img-pipeline-flow]

The accessibility pipeline at the moment has one step, which is run the  ADA Reporter script to analyze issues on several pages of the website. There is a fixed threshold for each page. If the number of errors is greater than this limit, the pipeline job fails.

![Accessibility Pipeline result][img-pipeline-result]

There is a plan to introduce a second step to this pipeline, which will execute accessibility functional tests.



# 9. Screen Readers

Screen readers convert digital text into synthesized speech. They empower users to hear content and navigate with the keyboard.

Some browsers seem to work better with certain screen readers:
- Firefox with [NVDA](https://nvaccess.org/download/)
- Chrome or Internet Explorer with [JAWS](https://freedomscientific.com/JAWSHQ/JAWSHeadquarters01)
- Safari with [VoiceOver](https://apple.com/accessibility/)
- Edge with [Narrator](https://microsoft.com/accessibility/windows)

(Source: [Webaim](https://webaim.org/techniques/screenreader/))



## 9.1. Voice Over

- Built into Apple Inc.'s macOS and iOS
- Free
- Open with: Command+F5
- Navigation:
  - Tab
  - Shift+Tab
  - Control+Option+Arrow
  - [See more](https://help.apple.com/voiceover/vo/en/VOKeysColor_1.html)



## 9.2. NVDA

- Windows 7 or superior
- Free (https://www.nvaccess.org/download/)
- Open with: Control+Alt+n
- Navigation:
  - Tab
  - Shift+Tab
  - [See more](http://www.accessiq.org/sites/default/files/nvda-keyboard-overlay_laptop_1670x1125.gif)


# 10. Most found issues and how to fix them

## 10.1. Alt text

Every image must have an alt attribute.

How to write appropriate alternative texts:
- Be accurate
- Be succinct
- Don't be redundant
- Don't use "image of" or "graphic of"

Decorative images still need an alt attribute, but it should be null (`alt=""`).

## 10.2. Duplicate ids

Duplicate values of type ID can be problematic for user agents that rely on this attribute to accurately convey relationships between different parts of content to users.

- Verify at the page if the new ID attribute that you're adding are not already in use.
- For dynamic components you may need to merge with item's id.

## 10.3. Links without href

Links must have a non-empty href attribute in order to be considered true links and to be accessible to keyboard users.

- Check if you couldn't use a button instead.
- Is not the best solution but you can go with `href="#"`.

## 10.4. Labels
Labels or instructions are provided when content requires user input.

- All labels should have a valid `for` attribute.
- There are some cases that you can use ARIA labeling properties:
  - aria-labelledby
  - aria-describedby
  - and aria-label


## 10.5. Modals
When dealing with modal windows the tab navigation should be restrained to the visible context, and when you leave this window you should take back to the preview's point.

- Use JavaScript to perform the "tabtrapping".
- With `document.activeElement` you can retrieve cursor position to redirect later.
- See [W3C modal example](https://www.w3.org/TR/wai-aria-practices-1.1/examples/dialog-modal/dialog.html) with the best practices



[img-wcag-standard]: https://github.com/saksdirect/frontend-manual/raw/master/accessibility-guidelines/imgs/wcag-standard.png "WCAG Standard"

[img-dashboard]: https://github.com/saksdirect/frontend-manual/raw/master/accessibility-guidelines/imgs/dashboard.png "Accessibility Dashboard"

[img-pipeline-flow]: https://github.com/saksdirect/frontend-manual/raw/master/accessibility-guidelines/imgs/pipeline-flow.png "Accessibility Pipeline flow"

[img-pipeline-result]: https://github.com/saksdirect/frontend-manual/raw/master/accessibility-guidelines/imgs/pipeline-result.png "Accessibility Pipeline result"
