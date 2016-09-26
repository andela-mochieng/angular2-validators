**NOTE** Still in development

[![npm version](https://badge.fury.io/js/angular2-validators.svg)](https://www.npmjs.com/package/angular2-validators)

# Ng2 Validators
A List of validators for Angular 2 Forms based on [validator.js](https://github.com/chriso/validator.js)

# Usage
## Install
```bash
$ npm install --save angular2-validators
```

## Use as Model Based Validators
```typescript
import { Component } from '@angular/core';

import { FormGroup, FormBuilder, Validators } from '@angular/forms';

import { isEmail } from 'angular2-validators';

@Component({
  selector: 'app-root',
  template: `
      <form [formGroup]="theForm" novalidate>
          <label for="name">Name</label>
          <input type="text" class="form-control" formControlName="name">
      </form>
  `,
})
export class AppComponent {
  theForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.theForm = fb.group({
      name: ['', [Validators.required, isEmail]]
    });
  }
}
```

## Use as Directive Validator
We need to import angular2-validators as a module in app.module.ts file, or equivalent
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { Ng2ValidatorsModule } from 'angular2-validators';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    ReactiveFormsModule,
    HttpModule,
    Ng2ValidatorsModule // Add angular2-validators module here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Then you can just use it in your template as a directive
```html
<input type="text" class="form-control" formControlName="name" isEmail>
```

## Contributing
This module is still in development and PRs are so welcome to the develop branch

## Added Validators
* contains(str, seed) - check if the string contains the seed
* equals(str, comparison) - check if the string matches the comparison.
* isAfter(str [, date]) - check if the string is a date that's after the specified date (defaults to now).
* isAlpha(str [, locale]) - check if the string contains only letters (a-zA-Z). Locale is one of `['ar', 'ar-AE', 'ar-BH', 'ar-DZ', 'ar-EG', 'ar-IQ', 'ar-JO', 'ar-KW', 'ar-LB', 'ar-LY', 'ar-MA', 'ar-QA', 'ar-QM', 'ar-SA', 'ar-SD', 'ar-SY', 'ar-TN', 'ar-YE', 'cs-CZ', 'de-DE', 'en-AU', 'en-GB', 'en-HK', 'en-IN', 'en-NZ', 'en-US', 'en-ZA', 'en-ZM', 'es-ES', 'fr-FR', 'hu-HU', 'nl-NL', 'pl-PL', 'pt-BR', 'pt-PT', 'ru-RU', 'sr-RS', 'sr-RS@latin', 'tr-TR']`) and defaults to `en-US`.
* isAlphanumeric(str [, locale]) - check if the string contains only letters and numbers. Locale is one of `['ar', 'ar-AE', 'ar-BH', 'ar-DZ', 'ar-EG', 'ar-IQ', 'ar-JO', 'ar-KW', 'ar-LB', 'ar-LY', 'ar-MA', 'ar-QA', 'ar-QM', 'ar-SA', 'ar-SD', 'ar-SY', 'ar-TN', 'ar-YE', 'cs-CZ', 'de-DE', 'en-AU', 'en-GB', 'en-HK', 'en-IN', 'en-NZ', 'en-US', 'en-ZA', 'en-ZM', 'es-ES', 'fr-FR', 'fr-BE', 'hu-HU', 'nl-BE', 'nl-NL', 'pl-PL', 'pt-BR', 'pt-PT', 'ru-RU', 'sr-RS', 'sr-RS@latin', 'tr-TR']`) and defaults to `en-US`.
* isAscii(str) - check if the string contains ASCII chars only.
* isBase64(str) - check if a string is base64 encoded.
* isBefore(str [, date]) - check if the string is a date that's before the specified date.
* isBoolean(str) - check if a string is a boolean.
* isByteLength(str, options) - check if the string's length (in bytes) falls in a range.`options` is an object which defaults to `{min:0, max: undefined}`.
* isCreditCard(str) - check if the string is a credit card.
* isCurrency(str, options) - check if the string is a valid currency amount. `options` is an object which defaults to `{symbol: '$', require_symbol: false, allow_space_after_symbol: false, symbol_after_digits: false, allow_negatives: true, parens_for_negatives: false, negative_sign_before_digits: false, negative_sign_after_digits: false, allow_negative_sign_placeholder: false, thousands_separator: ',', decimal_separator: '.', allow_space_after_digits: false }`.
* isDataUri(str) - check if the string is a [data uri format](https://developer.mozilla.org/en-US/docs/Web/HTTP/data_URIs).
* isDate(str) - check if the string is a date.
* isDecimal(str) - check if the string represents a decimal number, such as 0.1, .3, 1.1, 1.00003, 4.0, etc.
* isDivisibleBy(str, number) - check if the string is a number that's divisible by another.
* isEmail(str [, options]) - check if the string is an email. `options` is an object which defaults to `{ allow_display_name: false, allow_utf8_local_part: true, require_tld: true }`. If `allow_display_name` is set to true, the validator will also match `Display Name <email-address>`. If `allow_utf8_local_part` is set to false, the validator will not allow any non-English UTF8 character in email address' local part. If `require_tld` is set to false, e-mail addresses without having TLD in their domain will also be matched.
* isFloat(str [, options]) - check if the string is a float. `options` is an object which can contain the keys `min` and/or `max` to validate the float is within boundaries (e.g. `{ min: 7.22, max: 9.55 }`).
* isFQDN(str [, options]) - check if the string is a fully qualified domain name (e.g. domain.com). `options` is an object which defaults to `{ require_tld: true, allow_underscores: false, allow_trailing_dot: false }`.
* isFullWidth(str) - check if the string contains any full-width chars.
* isHalfWidth(str) - check if the string contains any half-width chars.
* isHexColor(str) - check if the string is a hexadecimal color
* isHexaDecimal(str) - check if the string is a hexadecimal number
* isInt(str, values) - check if the string is in a array of allowed values.
* isIP(str [, version]) - check if the string is an IP (version 4 or 6).
* isISBN(str [, version]) - check if the string is an ISBN (version 10 or 13).
* isISIN(str) - check if the string is an [ISIN][ISIN] (stock/security identifier).
* isISO6601(str) - check if the string is a valid [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date.
* isJSON(str) - check if the string is valid JSON (note: uses JSON.parse).
* isLength(str, options) - check if the string's length falls in a range. `options` is an object which defaults to `{min:0, max: undefined}`.
* isLowerCase(str) - check if the string is lowercase.
* isMacAddress(str) - check if the string is a MAC address.
* isMd5(str) - check if the string is a MD5 hash.
* isMobilePhone(str, locale) - check if the string is a mobile phone number, (locale is one of `['ar-DZ', 'ar-SA', 'ar-SY', 'cs-CZ', 'de-DE', 'da-DK', 'el-GR', 'en-AU', 'en-GB', 'en-HK', 'en-IN', 'en-NZ', 'en-US', 'en-CA', 'en-ZA', 'en-ZM', 'es-ES', 'fi-FI', 'fr-FR', 'hu-HU', 'it-IT', 'ja-JP', 'ms-MY', 'nb-NO', 'nn-NO', 'pl-PL', 'pt-PT', 'ru-RU', 'sr-RS', 'tr-TR', 'vi-VN', 'zh-CN', 'zh-TW']`).
* isMongoId(str) - check if the string is a valid hex-encoded representation of a [MongoDB ObjectId][mongoid].
* isMultibyte(str) - check if the string contains one or more multibyte chars.
* isNull(str) - check if the string is null (has a length of zero).
* isNumeric(str) - check if the string contains only numbers.
* isSurrogatePair(str) - check if the string contains any surrogate pairs chars.
* isUpperCase(str) - check if the string is uppercase.
* isURL(str [, options]) - check if the string is an URL. `options` is an object which defaults to `{ protocols: ['http','https','ftp'], require_tld: true, require_protocol: false, require_host: true, require_valid_protocol: true, allow_underscores: false, host_whitelist: false, host_blacklist: false, allow_trailing_dot: false, allow_protocol_relative_urls: false }`.
* isUUID(str [, version]) - check if the string is a UUID (version 3, 4 or 5).
* isVariableWidth(str) - check if the string contains a mixture of full and half-width chars.
* isWhiteListed(str, chars) - checks characters if they appear in the whitelist.



