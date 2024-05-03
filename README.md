
![minified size](https://badgen.net/bundlephobia/min/@kollorg/dolor-quidem-ducimus) ![minified zipped size](https://badgen.net/bundlephobia/minzip/@kollorg/dolor-quidem-ducimus) ![types](https://badgen.net/npm/types/@kollorg/dolor-quidem-ducimus) ![license](https://badgen.net/npm/license/@kollorg/dolor-quidem-ducimus) [![npm-publish](https://github.com/kollorg/dolor-quidem-ducimus/actions/workflows/npm-publish.yml/badge.svg)](https://github.com/kollorg/dolor-quidem-ducimus/actions/workflows/npm-publish.yml)

# Social Links

Social Links is helping to detect, validate and sanitize social (desktop & mobile) links

### Install
```bash
npm i @kollorg/dolor-quidem-ducimus --save
```

### Demo

- https://awesome-web-tools.web.app/@kollorg/dolor-quidem-ducimus - Example use case
- https://gkucmierz.github.io/@kollorg/dolor-quidem-ducimus-app - Detect profile demo (v1.7.0)

### Using
```js
import { SocialLinks, TYPE_MOBILE } from '@kollorg/dolor-quidem-ducimus';
const socialLinks = new SocialLinks();

const link = 'http://www.linkedin.com/in/gkucmierz';
const profileName = socialLinks.detectProfile(link); // 'linkedin'

console.log(socialLinks.isValid(profileName, link)); // true
console.log(socialLinks.sanitize(profileName, link)); // 'https://linkedin.com/in/gkucmierz'
console.log(socialLinks.sanitize(profileName, link, TYPE_MOBILE)); // 'https://linkedin.com/mwlite/in/gkucmierz'
```

Above examples works based on predefined **linkedin** profile:
```js
import { Profile } from '@kollorg/dolor-quidem-ducimus';
const linkedinProfile: Profile =
{ name: 'linkedin',
    matches: [
      {
        match: '(https?://)?(www.)?linkedin.com/in/({PROFILE_ID})', group: 3, type: TYPE_DESKTOP,
        pattern: 'https://linkedin.com/in/{PROFILE_ID}'
      },
      {
        match: '(https?://)?(www.)?linkedin.com/mwlite/in/({PROFILE_ID})', group: 3, type: TYPE_MOBILE,
        pattern: 'https://linkedin.com/mwlite/in/{PROFILE_ID}'
      },
      { match: '({PROFILE_ID})', group: 1 },
    ]
};
```

### Add new profile
```js
import { SocialLinks, Profile } from '@kollorg/dolor-quidem-ducimus';

const socialLinks = new SocialLinks();
const profileMatches: ProfileMatch[] = [ ... ];

socialLinks.addProfile('profileName', profileMatches);
```

### Configuration
```js
import { SocialLinks, Config } from '@kollorg/dolor-quidem-ducimus';

const config: Config = {
  usePredefinedProfiles: true,
  trimInput: true,
  allowQueryParams: false,
};
const socialLinks = new SocialLinks(config);
```

### Build

Watch, *tsc* build
```bash
npm run start
```

### Tests

Just *jest* tests
```bash
npm run test
```
or
```bash
npm run test:watch
```

### Contributing

[CONTRIBUTING.md](CONTRIBUTING.md)
