# Community Node Info Specification

**Version: 0.1.0**

This document describes the format of the information that should be supplied by the Community Node Service through the `resource_desc` URL for their account as recorded on-chain.

The data structure is [JSON](http://json-schema.org/specification.html).


<em> Note: The content of this section is based on the [OPES Community BP Information Standard](https://github.com/opes-community/data-schemas/tree/master/community-node-info) </em>

## Info Fields

### Info Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| title <br><em>String</em> | Title of the Community Node | 
| summary <br><em>String</em> | Short description of the organization operating the Community Node | 
| website <br><em>String</em> | URL of the Community Node's publicly accessible website | 
| producer_name <br><em>String</em> | Blockchain Name of the Community Node's Infrastructure Node account |
| org <br><em>Object</em> | Organization Object | 
| nodes <br><em>Array</em> | Array of Node Info Objects | 

### Organization Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| org_name <br><em>String</em>| Organization name |
| code_of_conduct <br><em>String</em> | URL pointing to the Community Node's Code of Conduct | 
| ownership_disclosure <br><em>String</em> | URL pointing to the Community Node's ownership documentation |
| email <br><em>String</em> | Contact Email for the Community Node | 
| branding <br><em>Object</em> | Branding Media Object |
| location <br><em>Object</em> | Location Object |
| social <br><em>Object</em> | Social Medias Object |


### Social Media Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| steemit <br><em>String</em>|  Steemit Username without @ |
| twitter <br><em>String</em>|  Twitter Username |
| youtube <br><em>String</em>|  YouTube Channel address |
| github  <br><em>String</em>|  GitHub Username |
| reddit  <br><em>String</em>|  Reddit Username |
| keybase <br><em>String</em>|  Keybase Username |
| telegram  <br><em>String</em>|  Telegram Username |
| wechat  <br><em>String</em>|  WeChat Username |

### Branding Media Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| logo_256 <br><em>String</em> | Fully qualified URL to a 256px by 256px logo image | 
| logo_1024 <br><em>String</em> | Fully qualified URL to a 1024px by 1024px logo image | 
| logo_svg <br><em>String</em> | Fully qualified URL to a SVG logo image | 

### Location Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| name <br><em>String</em> | Location in human-readable format (i.e. City, State/Province, Country) |
| country <br><em>String</em> | Two-digit country code in accordance to [ISO 3166-1 alpha-2](https://www.iso.org/iso-3166-country-codes.html) |
| latitude <br><em>String</em> | Latitude in decimal degrees | 
| longitude <br><em>String</em> | Longitude in decimal degrees | 

### Node Info Object

| Field <br><em>ValueType</em> | Description |
| --- | --- |
| location <br><em>Object</em> | Location Object |
| node_type <br><em>String</em> | Type of service the node provides, one of: <br>- <b>producer</b>: Node with block signing key <br>- <b>full</b>: Node in front of Producer to prevent malicious interactions <br>- <b>query</b>: Node that provides HTTP(S) API to the public <br>- <b>seed</b>: Node that provides P2P and/or BNET to the public |
| p2p_endpoint <br><em>String</em> | Peer to Peer Blockchain endpoint (`host:port`) |
| bnet_endpoint <br><em>String</em> | BNET Blockchain endpoint (`host:port`) |
| api_endpoint <br><em>String</em> | HTTP endpoint (`http://host:port`) |
| ssl_endpoint <br><em>String</em> | HTTPS endpoint (`https://host:port`) |


