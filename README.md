# Custom HTTP Headers Plugin

The **Custom HTTP Headers** Plugin is an extension for [Grav CMS](http://github.com/getgrav/grav). Provides the ability add custom HTTP Headers for Content Security Policy (CSP), Cross Origin Resource Sharing (CORS), Referrer-Policy, Permissions Policy, and other security needs.

## Installation

Installing the Custom HTTP Headers plugin can be done in one of three ways: The GPM (Grav Package Manager) installation method lets you quickly install the plugin with a simple terminal command, the manual method lets you do so via a zip file, and the admin method lets you do so via the Admin Plugin.

### GPM Installation (Preferred)

To install the plugin via the [GPM](http://learn.getgrav.org/advanced/grav-gpm), through your system's terminal (also called the command line), navigate to the root of your Grav-installation, and enter:

    bin/gpm install custom-http-headers

This will install the Custom HTTP Headers plugin into your `/user/plugins`-directory within Grav. Its files can be found under `/your/site/grav/user/plugins/custom-http-headers`.

### Manual Installation

To install the plugin manually, download the zip-version of this repository and unzip it under `/your/site/grav/user/plugins`. Then rename the folder to `custom-http-headers`. You can find these files on [GitHub](https://github.com/trilbymedia/grav-plugin-custom-http-headers) or via [GetGrav.org](http://getgrav.org/downloads/plugins#extras).

You should now have all the plugin files under

    /your/site/grav/user/plugins/custom-http-headers
	
> NOTE: This plugin is a modular component for Grav which may require other plugins to operate, please see its [blueprints.yaml-file on GitHub](https://github.com/trilbymedia/grav-plugin-custom-http-headers/blob/master/blueprints.yaml).

### Admin Plugin

If you use the Admin Plugin, you can install the plugin directly by browsing the `Plugins`-menu and clicking on the `Add` button.

## Configuration

Before configuring this plugin, you should copy the `user/plugins/custom-http-headers/custom-http-headers.yaml` to `user/config/plugins/custom-http-headers.yaml` and only edit that copy.

Here is the default configuration and an explanation of available options:

```yaml
enabled: true
enabled_in_admin: true
debug_headers: false
custom_headers:
  Content-Security-Policy: "upgrade-insecure-requests"
  Strict-Transport-Security: "max-age=2592000"
  X-Xss-Protection: "1; mode=block"
  X-Frame-Options: "DENY"
  X-Content-Type-Options: "nosniff"
  Referrer-Policy: "strict-origin-when-cross-origin"
  Permissions-Policy: "camera=(), geolocation=()"
remove_headers:
  - "Public-Key-Pins"
  - "X-Powered-By"
```

Note that if you use the Admin Plugin, a file with your configuration named custom-http-headers.yaml will be saved in the `user/config/plugins/`-folder once the configuration is saved in the Admin.

## Usage

Just enabling the plugin will allow it to respond to any request made through Grav.  Please note that this will not add custom headers for any requests made directly to the websever. CSS and JS requests, most image requests etc. are not processed through Grav.

There are certain headers that might be modified by the webserver after the response has been generated. If you want complete control you should use the headers mechanisms in your webserver as this is ultimately what is responsible for sending the response headers for any requests made to it.  

For more information on the various headers please check out:

- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
- https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS  
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers

## Debugging

You can debug the headers by enabling the `debug_headers:` option in the settings.  You must have the Grav debugger **enabled** and the resulting headers array will be displayed in teh **Messages** tab. 


