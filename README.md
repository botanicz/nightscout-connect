# nightscout-connect

Nightscout's methods for synchronizing with common diabetes cloud providers.
This module provides a single entry point to Nightscout for similar modules
and allows managing http library and injecting dependencies from a single
point.


## Work in progress

* Nightscout
  * [x] hello world
  * [x] better gap finding
  * [x] glucose
  * [ ] treatments, profiles, devicestatus
* [x] Dexcom
* [x] Glooko
  * [x] fetch data
  * [ ] translate data
* [ ] Diasend
* [ ] LibreLinkUp
* [ ] Medtronic
* [ ] Tandem

## Lower priority
* Better UI integration, diagnostics, test connection, fix errors, manage plugin...
* Generate predictable pattern eg sine for test.
* run in capture mode to generate up to date test fixtures
* better sidecar support
* better cli support (pipe to/from anywhere: `* | nightscout-connect | * `,
  file, fixtures, csv, json, web services...

## Help wanted
* more vendors
* better design suggestions
* testing


## Brief Doc
* `ENABLE=connect` include the keyword `connect` in the `ENABLE` list.
* Environment variable prefix `CONNECT_`:
  * `CONNECT_SOURCE` - The name for the source of one of the supported inputs.  one of `nightscout`, `dexcomshare`, etc...

### Nightscout

> Work in progress

To sync from another Nightscout site, include `CONNECT_SOURCE_ENDPOINT` and
`CONNECT_SOURCE_API_SECRET`. 
* `CONNECT_SOURCE=nightscout`
* `CONNECT_SOURCE_ENDPOINT=<URL>`
* `CONNECT_SOURCE_API_SECRET=<OPTIONAL_API_SECRET>`

The `CONNECT_SOURCE_ENDPOINT` must be a fully qualified URL and may contain a
`?token=<subject>` query string to specify an accessToken.
The `CONNECT_SOURCE_API_SECRET`, if provided, will be used to create a token
called `nightscout-connect-reader`.  This information or the token provided in
the query will be used to read information from Nightscout and is optional if
the site is readable by default.

Select this driver by setting `CONNECT_SOURCE` equal to `nightscout`.

### Dexcom Share
To synchronize from Dexcom Share use the following variables.
* `CONNECT_SOURCE=dexcomshare`
* `CONNECT_SHARE_ACCOUNT_NAME=`
* `CONNECT_SHARE_PASSWORD=`

Optional, `CONNECT_SHARE_REGION` and `CONNECT_SHARE_SERVER` do the same thing, only specify one.
* `CONNECT_SHARE_REGION=`  `ous` or `us`. `us` is the default if nothing is
  provided.  Selecting `us` sets `CONNECT_SHARE_SERVER` to `share2.dexcom.com`.
  Selecting `ous` here sets `CONNECT_SHARE_SERVER` to `shareous2.dexcom.com`.
* `CONNECT_SHARE_SERVER=` set the server domain to use.

### Glooko

> Note: Experimental.

To synchronize from Glooko use the following variables.
* `CONNECT_SOURCE=glooko`
* `CONNECT_GLOOKO_EMAIL=`
* `CONNECT_GLOOKO_PASSWORD=`

By default, `CONNECT_GLOOKO_SERVER` is set to `api.glooko.com` because the
default value for `CONNECT_GLOOKO_ENV` is `default`.
* `CONNECT_GLOOKO_ENV` is the word `default` by defalt.  Other values are
  `development`, `production`, for `api.glooko.work`, and
  `externalapi.glooko.com`, respectively.
* `CONNECT_GLOOKO_SERVER` the hostname server to use - `api.glooko.com` by `default`.

If both, `CONNECT_GLOOKO_SERVER` and `CONNECT_GLOOKO_ENV` are set, only
`CONNECT_GLOOKO_SERVER` will be used.



### `NEXT work in progress DRIVER`

