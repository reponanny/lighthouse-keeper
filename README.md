# Lighthouse Keeper

This tool uses Google’s [Lighthouse](https://github.com/GoogleChrome/lighthouse) under the hood and gives the possibility to scan a list of URLs and get the result of specific audits.

## Installation

```bash
npm install --save-dev @sum.cumo/lighthouse-keeper
```

### Google Chrome

You need a [Chrome installation](https://developers.google.com/web/updates/2017/04/headless-chrome) in order to be able to execute lighthouse.

## Usage

### With JSON Config File

```bash
lighthouse-keeper --config path/to/config.json
```

#### Options

These are the possible options for the configuration file:

| Option        | Description   | Default |
| ------------- | ------------- | ------------- |
| urls | array of urls to scan (max. 6) | `[]` |
| extendedInfo | display extended info of the audit | `false` by default. If the audit is not satisfied extendInfo turns true |
| allAudits| indicates if all audits should be evaluated | `false` |
| onlyAudits| array of audit keys to evaluate (see below) | `[]` |
| scores| object of minimum scores per category (see below) to obtain | `{}` |

#### Example

```json
{
  "urls": [
    "https://www.example.com/"
  ],
  "scores": {
    "performance": 90,
    "accessibility": 90,
    "best-practices": 90,
    "seo": 80
  },
  "onlyCategories": [
    "performance",
    "accessibility",
    "best-practices",
    "seo"
  ],
  "skipAudits": [
    "byte-efficiency/uses-responsive-images",
    "byte-efficiency/uses-webp-images",
    "seo/meta-description"
  ],
  "extendedInfo": true
}
```

### Without Config File

```bash
lighthouse-keeper --url https://www.example.com --audits accesskeys,uses-http2 --scores seo:90,best-practices:10
```

These are the possible options for the CLI.

| Option        | Description   | Mandatory |
| ------------- | ------------- | ------------- |
| url | the url to scan | yes |
| audits| list of audits that should be evaluated (see below) | no |
| scores| list of minimum scores per category to obtain (see below) | no |
| showaudits| only show the available audits | no |

All list entries can be divided by a comma.

### Categories

| Category ID   | Description   |
| ------------- | ------------- |
| accessibility | These checks highlight opportunities to [improve the accessibility of your web app](https://developers.google.com/web/fundamentals/accessibility). Only a subset of accessibility issues can be automatically detected so manual testing is also encouraged. |
| best-practices | We’ve compiled some recommendations for modernizing your web app and avoiding performance pitfalls. |
| performance | These encapsulate your web app’s current performance and opportunities to improve it. |
| pwa | These checks validate the aspects of a Progressive Web App, as specified by the baseline [PWA Checklist](https://developers.google.com/web/progressive-web-apps/checklist). |
| seo | These checks ensure that your page is optimized for search engine results ranking. There are additional factors Lighthouse does not check that may affect your search ranking. [Learn more](https://support.google.com/webmasters/answer/35769). |

### Audits

If you want to see a list of all available audits, run

```bash
lighthouse-keeper --url https://www.example.com/ --showaudits
```

The `url` is actually irrelevant for the list, but needed for running Lighthouse to parse the response in order to get the list.

Please have in mind that there are audits like `screenshot-thumbnails` which can’t be validated. These audits are marked with a `⚠` in the audits list and with `(?)` in the result.

## License

Copyright 2018 [sum.cumo GmbH](https://www.sumcumo.com/)

Licensed under the Apache License, Version 2.0 (the “License”); you may not use this file except in compliance with the License. You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an “AS IS” BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
