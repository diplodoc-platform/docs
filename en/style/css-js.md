# Connecting CSS and JavaScript

{% note warning %}

Free inclusion of JavaScript files is only allowed in static builds.

{% endnote %}

CSS styles and JavaScript files allow you to adapt the design and add interactivity to the documentation — from fine-tuning individual elements to creating a unique visual style and behavior.

To connect your style or script to the project:

1. In the project root, create a file with the style or script, for example:  
   - for css: `_assets/style/custom.css`  
   - for js: `_assets/script/custom.js`
2. Add the CSS or JavaScript code to the corresponding file.
3. In the configuration file `.yfm`, add the required block:
    ```yaml
    resources:
      style:
        - _assets/style/custom.css
      script:
        - _assets/script/custom.js
    ```
4. Build the project with the flag `--allow-custom-resources`.

For an example of using styles, see the [Diplodoc repository](https://github.com/diplodoc-platform/docs).
