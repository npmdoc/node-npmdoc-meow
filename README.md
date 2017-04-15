# api documentation for  [meow (v3.7.0)](https://github.com/sindresorhus/meow#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-meow.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-meow) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-meow.svg)](https://travis-ci.org/npmdoc/node-npmdoc-meow)
#### CLI app helper

[![NPM](https://nodei.co/npm/meow.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/meow)

[![apidoc](https://npmdoc.github.io/node-npmdoc-meow/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-meow/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-meow/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-meow/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sindre Sorhus",
        "url": "sindresorhus.com"
    },
    "bugs": {
        "url": "https://github.com/sindresorhus/meow/issues"
    },
    "dependencies": {
        "camelcase-keys": "^2.0.0",
        "decamelize": "^1.1.2",
        "loud-rejection": "^1.0.0",
        "map-obj": "^1.0.1",
        "minimist": "^1.1.3",
        "normalize-package-data": "^2.3.4",
        "object-assign": "^4.0.1",
        "read-pkg-up": "^1.0.1",
        "redent": "^1.0.0",
        "trim-newlines": "^1.0.0"
    },
    "description": "CLI app helper",
    "devDependencies": {
        "ava": "*",
        "execa": "^0.1.1",
        "indent-string": "^2.1.0",
        "xo": "*"
    },
    "directories": {},
    "dist": {
        "shasum": "72cb668b425228290abbfa856892587308a801fb",
        "tarball": "https://registry.npmjs.org/meow/-/meow-3.7.0.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "9a5c90af79fb8f5f29c97e6b92b63f41e2df4f34",
    "homepage": "https://github.com/sindresorhus/meow#readme",
    "keywords": [
        "cli",
        "bin",
        "util",
        "utility",
        "helper",
        "argv",
        "command",
        "line",
        "meow",
        "cat",
        "kitten",
        "parser",
        "option",
        "flags",
        "input",
        "cmd",
        "console"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "sindresorhus"
        }
    ],
    "name": "meow",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/sindresorhus/meow.git"
    },
    "scripts": {
        "test": "xo && ava"
    },
    "version": "3.7.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module meow](#apidoc.module.meow)
1.  [function <span class="apidocSignatureSpan"></span>meow (opts, minimistOpts)](#apidoc.element.meow.meow)
1.  [function <span class="apidocSignatureSpan">meow.</span>toString ()](#apidoc.element.meow.toString)



# <a name="apidoc.module.meow"></a>[module meow](#apidoc.module.meow)

#### <a name="apidoc.element.meow.meow"></a>[function <span class="apidocSignatureSpan"></span>meow (opts, minimistOpts)](#apidoc.element.meow.meow)
- description and source-code
```javascript
meow = function (opts, minimistOpts) {
	loudRejection();

	if (Array.isArray(opts) || typeof opts === 'string') {
		opts = {help: opts};
	}

	opts = objectAssign({
		pkg: readPkgUp.sync({
			cwd: parentDir,
			normalize: false
		}).pkg,
		argv: process.argv.slice(2)
	}, opts);

	minimistOpts = objectAssign({}, minimistOpts);

	minimistOpts.default = mapObj(minimistOpts.default || {}, function (key, value) {
		return [decamelize(key, '-'), value];
	});

	if (Array.isArray(opts.help)) {
		opts.help = opts.help.join('\n');
	}

	var pkg = typeof opts.pkg === 'string' ? require(path.join(parentDir, opts.pkg)) : opts.pkg;
	var argv = minimist(opts.argv, minimistOpts);
	var help = redent(trimNewlines(opts.help || ''), 2);

	normalizePackageData(pkg);

	process.title = pkg.bin ? Object.keys(pkg.bin)[0] : pkg.name;

	var description = opts.description;
	if (!description && description !== false) {
		description = pkg.description;
	}

	help = (description ? '\n  ' + description + '\n' : '') + (help ? '\n' + help : '\n');

	var showHelp = function (code) {
		console.log(help);
		process.exit(code || 0);
	};

	if (argv.version && opts.version !== false) {
		console.log(typeof opts.version === 'string' ? opts.version : pkg.version);
		process.exit();
	}

	if (argv.help && opts.help !== false) {
		showHelp();
	}

	var _ = argv._;
	delete argv._;

	return {
		input: _,
		flags: camelcaseKeys(argv),
		pkg: pkg,
		help: help,
		showHelp: showHelp
	};
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.meow.toString"></a>[function <span class="apidocSignatureSpan">meow.</span>toString ()](#apidoc.element.meow.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
