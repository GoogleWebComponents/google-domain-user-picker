## google-domain-user-picker

Easily choose a user from a Google Apps Domain.

Built with [Polymer](https://polymer-project.org).

## Installation

```
bower install --save GoogleWebComponents/google-domain-user-picker
```

then import it like so

```html
<link rel="import" href="../google-domain-user-picker/google-domain-user-picker.html">
```

## Usage

With an access_token

```html
<google-domain-user-picker access-token="<my_token>"
                           on-select-user="onUserSelected">
</google-domain-user-picker>
```

or, with [google-signin](https://github.com/GoogleWebComponents/google-signin)

```html
<google-domain-user-picker on-select-user="onUserSelected">
</google-domain-user-picker>
```

Check out the [demo pages](demo) for more detailed examples.

## Details

**The demos have detailed usage within and outside of a Polymer app/element.**

Available properties:

<table>
  <tr>
    <th>Property</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>accessToken</td>
    <td>the accessToken that will be used when making authenticated requests to the Google Admin SDK API</td>
  </tr>
  <tr>
    <td>placeholder</td>
    <td>placeholder text for the main input element</td>
  </tr>
  <tr>
    <td>minLength</td>
    <td>minimum input text required to search for a user</td>
  </tr>
  <tr>
    <td>maxResults</td>
    <td>the maximum number of results to show</td>
  </tr>
  <tr>
    <td>lastUser</td>
    <td>the last user chosen from the input</td>
  </tr>
  <tr>
    <td>value</td>
    <td>current value of the input - settable and gettable</td>
  </tr>
  <tr>
    <td>defaultProfileImage</td>
    <td>image url shown when a user does not have a profile picture</td>
  </tr>
</table>

Available methods:

<table>
  <tr>
    <th>Method</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>clearResults</td>
    <td>clears the results of the picker</td>
  </tr>
</table>

Available events:

<table>
  <tr>
    <th>Event</th>
    <th>Description</th>
    <th>Format</th>
  </tr>
  <tr>
    <td>select-user</td>
    <td>fired when a user is selected by the mouse or enter key</td>
    <td>{name: String, email: String, id: String, image: String}</td>
  </tr>
  <tr>
    <td>focus-user</td>
    <td>fired when a user is focused by the mouse or arrow keys</td>
    <td>{name: String, email: String, id: String, image: String}</td>
  </tr>
  <tr>
    <td>error</td>
    <td>fired when there is an error with the picker</td>
    <td>String</td>
  </tr>
</table>

The provided access token must have the `https://www.googleapis.com/auth/admin.directory.user.readonly` scope.

## Apps Script

`google-domain-user-picker` can also be used within a Google Apps Script add-on with some additional setup. To use this component in your Apps Script add-on:

Include the element and the webcomponents shim. **These must be served over https.**

```html
<script src="https://example.com/webcomponentsjs/webcomponents-lite.js"></script>
<link rel="import" href="https://example.com/google-domain-user-picker/google-domain-user-picker.html">
```

In your `Code.gs`, create a function that returns the user's access_token.

```js
function accessToken() {
  return ScriptApp.getOAuthToken();
}
```

On your client side javascript, acquire this token via

```js
google.script.run.withSuccessHandler(function(accessToken) {
  document.querySelector('google-domain-user-picker').setAttribute('access-token', accessToken);
}).accessToken();
```
An important note is that to request the `https://www.googleapis.com/auth/admin.directory.user.readonly` scope, your Apps Script add-on must pretend to access that service through Apps Script itself.

To do this, follow [this guide to enable the AdminDirectory service](https://developers.google.com/apps-script/guides/services/advanced).

Then create a function in `Code.gs` like so:

```js
function fakeAdminDirectoryCall() {
  AdminDirectory.Users.list();
}
```

There's no need to ever run that function, unless you'd like to; `google-domain-user-picker` handles talking to the Admin Directory API.

## License

```
Copyright 2015 Google Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
