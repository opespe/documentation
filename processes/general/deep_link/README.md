# OPES Deep Link / QR Code Specification

In order to generate activity between an Access Node (AN) and a Personal Node (PN),
we use a deep link configured and provided by the AN. With that link, the PN can
initiate communication with the AN and, between the two, generate and send an
activity tally into the system.
```
IMPORTANT: This document describes the current specification,
           but you should expect that this specification will change in the future.
```
## Deep Link Query Parameters

In order to generate the deep link and QR code, the following values must be
determined.

| Value | Description |
| ---- | ---- | 
| host [REQUIRED] | The deep link host. Currently, the only valid value is `mobile.opes.pe`. |
| action [REQUIRED] | The action to initiate between AN and PN. Currently, the only valid value is `check-in`. |
| url [REQUIRED] | The URL-encoded URL of the Access Node. |
| name [REQUIRED] | The URL-encoded display name of the Access Node. This is only for display purposes, but should reflect the AN identity. |
| source [OPTIONAL] | A URL-encoded string. This string (prior to URL-encoding) should be at most 16 ASCII characters in length. It is possible that, post URL-encoding, this value may exceed 16 characters. This string is not required for standard behaviors, but will be returned to the Access Node when the action is triggered, and so can represent (as an id) any data the Access Node holds. Example: place a tracking id in this parameter to identify campaign, channel, etc. |
| ref | A value to identify the context of the deep link. A deep link _per se_ should *not* include this parameter, but a link encoded into a QR code *should* include this parameter with the value `qrcode`. |

## Building the Link

Given values determined above, the base deep link URL is built as such:
```
 https://{host}/opesapp/{action}
         ?url={url}
         &name={name}
         &source={source}
         &ref={ref}
```
NOTE: The deep links depicted here and later are split across multiple lines for readability.
      Your actual link should be a single line without whitespace.

Keep in mind that the `ref` query parameter must only be used if encoding into a QR code.

## Example

For these query parameter values:

|Parameter      | Value                       | URL-Encoded Value
| ----          | -------                     | -----------
|host           | `mobile.opes.pe`            | n/a
|action         | `check-in`                  | n/a
|url            | `\https://access.opes.one`  | `https%3A%2F%2Faccess.opes.one`
|name           | `OpesONE`                   | `OpesONE`
|source         | `T5W:B6A:N9`                | `T5W%3AB6A%3AN9`
|ref            | `qrcode`                    | n/a

Building a deep link for a web page generates the following. (Note the lack of a `ref` query parameter.)
```
 https://mobile.opes.pe/opesapp/check-in
     ?url=https%3A%2F%2Faccess.opes.one&name=OpesONE&source=T5W%3AB6A%3AN9
```
The above is intended for general use, including embedding it as a link on a web page.
If you want to encode that deep link into a QR code, append the `ref=qrcode` parameter
before encoding it as a QR code.
```
 https://mobile.opes.pe/opesapp/check-in
     ?url=https%3A%2F%2Faccess.opes.one&name=OpesONE&source=T5W%3AB6A%3AN9&ref=qrcode
```
Use this QR-specific link in your favorite QR code generation tool to build your
QR codes.
