# letsencrypt-alwaysdata

Update your SSL certs on alwaysdata via their REST API.

It requires you to have the following binaries installed and available in your `$PATH`:

- [`simp_le`](https://forum.alwaysdata.com/viewtopic.php?id=4631) (to call letsencrypt API);
- [`jq`](https://stedolan.github.io/jq/) (to parse and builds REST payloads).

# Install

Run the following from an alwaysadata shared hosting shell:

```bash
git clone https://github.com/oncletom/letsencrypt-alwaysdata.git
cd letsencrypt-alwaysdata

mkdir -p $HOME/.local/bin
ln -s update-certificate $HOME/.local/bin/update-certificate
```

# Use

```bash
update-certificate \
  --cert-name example.com \
  --site-dir $HOME/www \
  --letsencrypt-options "-d example.com -d www.example.com"
```

This is ideal to setup as a cronjob in order to execute `update-certificate` to renew your cert on time, automatically.

`ALWAYSDATA_API_AUTH` environment variable must be set prior to running the script (and can be found under the [Profile section](https://admin.alwaysdata.com/admin/details/)). This way we avoid leaking the API key in your `history` logs.

```bash
cat /path/to/.env
>> export ALWAYSDATA_API_AUTH="<api-key> account=<some-account>:"

source /path/to/.env
update-certificate ...
```

## `--cert-name`

This is the name of the certificate as found in the Alwaysdata admin interface.

Example: `--cert-name sudweb.fr`.

![](alwaysdata-certificate-admin.png)

## `--site-dir`

This is the location of the website served by the certificate.

Example: `--site-dir $HOME/www`.

## `--letsencrypt-options`

Any other option you would like to pass to letsencrypt, like your domains and eventually their individual mapping.

Example: `--letsencrypt-options "-d sudweb.fr -d www.sudweb.fr -d estcequecestientot.sudweb.fr:$HOME/estcequecestbientot"`.

# License 

> The MIT License (MIT)
> Copyright (c) 2016 Thomas Parisot
> 
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
> 
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
> 
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
