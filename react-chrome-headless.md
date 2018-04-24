# How to use chrome --headless with React apps

I was trying to use Chrome cli to debug an issue with Puppeteer. But cli only
showed initial server-side rendered page:

```
~/melissachang.github.io (master): google-chrome --headless --dump-dom http://localhost:4400
<snip>
</style></head>
  <body>
    <noscript>
      You need to enable JavaScript to run this app.
    </noscript>
    <div id="root"><div></div></div>
    <!--
      This HTML file is a template.
      If you open it directly in the browser, you will see an empty page.

      You can add webfonts, meta tags, or analytics to this file.
      The build step will place the bundled scripts into the <body> tag.

      To begin the development, run `npm start` or `yarn start`.
      To create a production bundle, use `npm run build` or `yarn build`.
    -->
  <script type="text/javascript" src="/static/js/bundle.js"></script>

</body></html>
```
Workaround is to use --repl to execute Javascript. Replacing `--dump-dom` with `--repl` results in an infinite loop. Fortunately, someone gave a workaround (search for "undefined" [here](https://developers.google.com/web/updates/2017/04/headless-chrome)).
```
/opt/google/chrome/chrome --headless --repl http://localhost:4400
```
Then `document.body.innerHTML` works as expected.
