# Is this a nunjucks bug or is it just me?

Run:

    npm install
    node nunjuckstest.js

Program crashes with:

    Template render error: (/Users/boutell/src/nunjucks-bug/views/report.html)
      TypeError: Object [object Object] has no method 'rootRenderFunc'
        at Object.exports.withPrettyErrors (/Users/boutell/src/nunjucks-bug/node_modules/nunjucks/src/lib.js:31:17)
        at Object.extend.render (/Users/boutell/src/nunjucks-bug/node_modules/nunjucks/src/environment.js:300:20)
        at Object.<anonymous> (/Users/boutell/src/nunjucks-bug/nunjuckstest.js:6:24)
        at Module._compile (module.js:456:26)
        at Object.Module._extensions..js (module.js:474:10)
        at Module.load (module.js:356:32)
        at Function.Module._load (module.js:312:12)
        at Function.Module.runMain (module.js:497:10)
        at startup (node.js:119:16)
        at node.js:901:3

I get different errors if report.html or index.html does not exist, so it seems to have to do with extends.

`nunjuckstest.js` is:

    var nunjucks = require('nunjucks');

    var env = new nunjucks.Environment(new nunjucks.FileSystemLoader(__dirname + '/views'));
    var indexTmpl = env.getTemplate('index.html');
    var reportTmpl = env.getTemplate('report.html');
    console.log(reportTmpl.render({}));

`index.html` is just:

    {% block body %}
    {% endblock %}

`report.html` is just:

    {% extends "index.html" %}

    {% block body %}
    <h2>Test</h2>
    {% endblock %}

Thanks!

`tom@punkave.com`
