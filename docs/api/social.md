---
id: social
title: utils.social
---
<a name="social"></a>

A namespace that contains various utilities to help you extract social handles
from text, URLs and and HTML documents.

**Example usage:**

```javascript
const Apify = require('apify');

const emails = Apify.utils.social.emailsFromText('alice@example.com bob@example.com');
```


* [`social`](#social) : <code>object</code>
    * [`.LINKEDIN_REGEX`](#social.LINKEDIN_REGEX) : <code>RegExp</code>
    * [`.LINKEDIN_REGEX_GLOBAL`](#social.LINKEDIN_REGEX_GLOBAL) : <code>RegExp</code>
    * [`.INSTAGRAM_REGEX`](#social.INSTAGRAM_REGEX) : <code>RegExp</code>
    * [`.INSTAGRAM_REGEX_GLOBAL`](#social.INSTAGRAM_REGEX_GLOBAL) : <code>RegExp</code>
    * [`.TWITTER_REGEX`](#social.TWITTER_REGEX) : <code>RegExp</code>
    * [`.TWITTER_REGEX_GLOBAL`](#social.TWITTER_REGEX_GLOBAL) : <code>RegExp</code>
    * [`.FACEBOOK_REGEX`](#social.FACEBOOK_REGEX) : <code>RegExp</code>
    * [`.FACEBOOK_REGEX_GLOBAL`](#social.FACEBOOK_REGEX_GLOBAL) : <code>RegExp</code>
    * [`.EMAIL_REGEX`](#social.EMAIL_REGEX) : <code>RegExp</code>
    * [`.EMAIL_REGEX_GLOBAL`](#social.EMAIL_REGEX_GLOBAL) : <code>RegExp</code>
    * [`.emailsFromText(text)`](#social.emailsFromText) ⇒ <code>Array&lt;String&gt;</code>
    * [`.emailsFromUrls(urls)`](#social.emailsFromUrls) ⇒ <code>Array&lt;String&gt;</code>
    * [`.phonesFromText(text)`](#social.phonesFromText) ⇒ <code>Array&lt;String&gt;</code>
    * [`.phonesFromUrls(urls)`](#social.phonesFromUrls) ⇒ <code>Array&lt;String&gt;</code>

<a name="social.LINKEDIN_REGEX"></a>

## `social.LINKEDIN\_REGEX` : <code>RegExp</code>
Regular expression to exactly match a single LinkedIn profile URL.
It has the following form: `/^...$/i` and matches URLs such as:
```
https://www.linkedin.com/in/alan-turing
en.linkedin.com/in/alan-turing
linkedin.com/in/alan-turing
```

The regular expression does NOT match URLs with additional
subdirectories or query parameters, such as:
```
https://www.linkedin.com/in/linus-torvalds/latest-activity
```

Example usage:
```
if (Apify.utils.social.LINKEDIN_REGEX.test('https://www.linkedin.com/in/alan-turing')) {
    console.log('Match!');
}
```

<a name="social.LINKEDIN_REGEX_GLOBAL"></a>

## `social.LINKEDIN\_REGEX\_GLOBAL` : <code>RegExp</code>
Regular expression to find multiple LinkedIn profile URLs in a text or HTML.
It has the following form: `/.../ig` and matches URLs such as:
```
https://www.linkedin.com/in/alan-turing
en.linkedin.com/in/alan-turing
linkedin.com/in/alan-turing
```

If the profile URL contains subdirectories or query parameters, the regular expression
extracts just the base part of the profile URL. For example, from text such as:
```
https://www.linkedin.com/in/linus-torvalds/latest-activity
```
the expression extracts just the following base URL:
```
https://www.linkedin.com/in/linus-torvalds
```

Example usage:
```
const matches = text.match(Apify.utils.social.LINKEDIN_REGEX_GLOBAL);
if (matches) console.log(`${matches.length} LinkedIn profiles found!`);
```

<a name="social.INSTAGRAM_REGEX"></a>

## `social.INSTAGRAM\_REGEX` : <code>RegExp</code>
Regular expression to exactly match a single Instagram profile URL.
It has the following form: `/^...$/i` and matches URLs such as:
```
https://www.instagram.com/old_prague
www.instagram.com/old_prague/
instagr.am/old_prague
```

The regular expression does NOT match URLs with additional
subdirectories or query parameters, such as:
```
https://www.instagram.com/cristiano/followers
```

Example usage:
```
if (Apify.utils.social.INSTAGRAM_REGEX_STRING.test('https://www.instagram.com/old_prague')) {
    console.log('Match!');
}
```

<a name="social.INSTAGRAM_REGEX_GLOBAL"></a>

## `social.INSTAGRAM\_REGEX\_GLOBAL` : <code>RegExp</code>
Regular expression to find multiple Instagram profile URLs in a text or HTML.
It has the following form: `/.../ig` and matches URLs such as:
```
https://www.instagram.com/old_prague
www.instagram.com/old_prague/
instagr.am/old_prague
```

If the profile URL contains subdirectories or query parameters, the regular expression
extracts just the base part of the profile URL. For example, from text such as:
```
https://www.instagram.com/cristiano/followers
```
the expression extracts just the following base URL:
```
https://www.instagram.com/cristiano
```

Example usage:
```
const matches = text.match(Apify.utils.social.INSTAGRAM_REGEX_GLOBAL);
if (matches) console.log(`${matches.length} Instagram profiles found!`);
```

<a name="social.TWITTER_REGEX"></a>

## `social.TWITTER\_REGEX` : <code>RegExp</code>
Regular expression to exactly match a single Twitter profile URL.
It has the following form: `/^...$/i` and matches URLs such as:
```
https://www.twitter.com/apify
twitter.com/apify
```

The regular expression does NOT match URLs with additional
subdirectories or query parameters, such as:
```
https://www.twitter.com/realdonaldtrump/following
```

Example usage:
```
if (Apify.utils.social.TWITTER_REGEX_STRING.test('https://www.twitter.com/apify')) {
    console.log('Match!');
}
```

<a name="social.TWITTER_REGEX_GLOBAL"></a>

## `social.TWITTER\_REGEX\_GLOBAL` : <code>RegExp</code>
Regular expression to find multiple Twitter profile URLs in a text or HTML.
It has the following form: `/.../ig` and matches URLs such as:
```
https://www.twitter.com/apify
twitter.com/apify
```

If the profile URL contains subdirectories or query parameters, the regular expression
extracts just the base part of the profile URL. For example, from text such as:
```
https://www.twitter.com/realdonaldtrump/following
```
the expression extracts only the following base URL:
```
https://www.twitter.com/realdonaldtrump
```

Example usage:
```
const matches = text.match(Apify.utils.social.TWITTER_REGEX_STRING);
if (matches) console.log(`${matches.length} Twitter profiles found!`);
```

<a name="social.FACEBOOK_REGEX"></a>

## `social.FACEBOOK\_REGEX` : <code>RegExp</code>
Regular expression to exactly match a single Facebook profile URL.
It has the following form: `/^...$/i` and matches URLs such as:
```
https://www.facebook.com/apifytech
facebook.com/apifytech
fb.com/apifytech
https://www.facebook.com/profile.php?id=123456789
```

The regular expression does NOT match URLs with additional
subdirectories or query parameters, such as:
```
https://www.facebook.com/apifytech/photos
```

Example usage:
```
if (Apify.utils.social.FACEBOOK_REGEX_STRING.test('https://www.facebook.com/apifytech')) {
    console.log('Match!');
}
```

<a name="social.FACEBOOK_REGEX_GLOBAL"></a>

## `social.FACEBOOK\_REGEX\_GLOBAL` : <code>RegExp</code>
Regular expression to find multiple Facebook profile URLs in a text or HTML.
It has the following form: `/.../ig` and matches URLs such as:
```
https://www.facebook.com/apifytech
facebook.com/apifytech
fb.com/apifytech
```

If the profile URL contains subdirectories or query parameters, the regular expression
extracts just the base part of the profile URL. For example, from text such as:
```
https://www.facebook.com/apifytech/photos
```
the expression extracts only the following base URL:
```
https://www.facebook.com/apifytech
```

Example usage:
```
const matches = text.match(Apify.utils.social.FACEBOOK_REGEX_GLOBAL);
if (matches) console.log(`${matches.length} Facebook profiles found!`);
```

<a name="social.EMAIL_REGEX"></a>

## `social.EMAIL\_REGEX` : <code>RegExp</code>
Regular expression to exactly match a single email address.
It has the following form: `/^...$/i`.

<a name="social.EMAIL_REGEX_GLOBAL"></a>

## `social.EMAIL\_REGEX\_GLOBAL` : <code>RegExp</code>
Regular expression to find multiple email addresses in a text.
It has the following form: `/.../ig`.

<a name="social.emailsFromText"></a>

## `social.emailsFromText(text)` ⇒ <code>Array&lt;String&gt;</code>
The function extracts email addresses from a plain text.
Note that the function preserves the order of emails and keep duplicates.

**Returns**: <code>Array&lt;String&gt;</code> - Array of emails addresses found.
If no emails are found, the function returns an empty array.  
<table>
<thead>
<tr>
<th>Param</th><th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>text</code></td><td><code>String</code></td>
</tr>
<tr>
<td colspan="3"><p>Text to search in.</p>
</td></tr></tbody>
</table>
<a name="social.emailsFromUrls"></a>

## `social.emailsFromUrls(urls)` ⇒ <code>Array&lt;String&gt;</code>
The function extracts email addresses from a list of URLs.
Basically it looks for all `mailto:` URLs and returns valid email addresses from them.
Note that the function preserves the order of emails and keep duplicates.

**Returns**: <code>Array&lt;String&gt;</code> - Array of emails addresses found.
If no emails are found, the function returns an empty array.  
<table>
<thead>
<tr>
<th>Param</th><th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>urls</code></td><td><code>Array&lt;String&gt;</code></td>
</tr>
<tr>
<td colspan="3"><p>Array of URLs.</p>
</td></tr></tbody>
</table>
<a name="social.phonesFromText"></a>

## `social.phonesFromText(text)` ⇒ <code>Array&lt;String&gt;</code>
The function attempts to extract phone numbers from a text. Please note that
the results might not be accurate, since phone numbers appear in a large variety of formats and conventions.
If you encounter some problems, please [file an issue](https://github.com/apifytech/apify-js/issues).

**Returns**: <code>Array&lt;String&gt;</code> - Array of phone numbers found.
If no phone numbers are found, the function returns an empty array.  
<table>
<thead>
<tr>
<th>Param</th><th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>text</code></td><td><code>String</code></td>
</tr>
<tr>
<td colspan="3"><p>Text to search the phone numbers in.</p>
</td></tr></tbody>
</table>
<a name="social.phonesFromUrls"></a>

## `social.phonesFromUrls(urls)` ⇒ <code>Array&lt;String&gt;</code>
Finds phone number links in an array of URLs and extracts the phone numbers from them.
Note that the phone number links look like `tel://123456789`, `tel:/123456789` or `tel:123456789`.

**Returns**: <code>Array&lt;String&gt;</code> - Array of phone numbers found.
If no phone numbers are found, the function returns an empty array.  
<table>
<thead>
<tr>
<th>Param</th><th>Type</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>urls</code></td><td><code>Array&lt;String&gt;</code></td>
</tr>
<tr>
<td colspan="3"><p>Array of URLs.</p>
</td></tr></tbody>
</table>
