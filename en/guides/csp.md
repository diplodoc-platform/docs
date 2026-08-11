# Managing Content Security Policy (CSP)

CSP is a tool for preventing various attacks, such as XSS (cross-site scripting), and other security threats.

To configure CSP policies, add the relevant settings to the .yfm file. This allows you to manage in detail the allowed sources for various types of resources.

#### Usage example:

```yaml
resources:
  csp:
    - "frame-src":
        - "https://test.site"
```

In this example, we allow loading frames only from <https://test.site>. You can add your own rules and sources to ensure security compliance specifically for your documentation.

#### Disabling CSP {#disable-csp}

If CSP is managed externally (for example, via server HTTP headers), you can completely disable adding the CSP meta tag during the build.

Via the configuration file `.yfm`:

```yaml
disableCsp: true
```

Or via a CLI argument:

```bash
yfm build --disable-csp -i ./input -o ./output
```

When this parameter is enabled, the meta tag `<meta http-equiv="Content-Security-Policy">` will not be added to any page, including pages with connected extensions (for example, neuroExpert).

More about CSP: <https://content-security-policy.com/>