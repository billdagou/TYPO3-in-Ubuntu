#Ubuntu 16.04♥中的TYPO3 —— Node.js

*Node.js对TYPO3本身来说，不是什么必须的功能，只是借助Grunt及相关插件对.css和.js进行相应的管理*

从[Node.js官网](https://nodejs.org/en/download/)下载Node.js并安装

详细安装步骤请参考 [这里](http://gruntjs.com/getting-started)

*以下步骤默认在开发目录下操作*

以命令行模式运行 `npm install`，根据提示创建 `package.json`

	{
		"description": "Project description here...",
		"repository": {},
		"README": "",
		"license": "GPL-2.0"
	}

全局安装 `grunt-cli`

	npm install -g grunt-cli

安装`grunt` 并保存至 `package.json` 中

	npm install grunt --save-dev

安装css（以 `grunt-contrib-stylus` 为例）、js（以 `grunt-contrib-uglify` 为例）、任务监控（以 `grunt-contrib-watch`为例）相关插件，并保存至 `package.json` 中

	npm install grunt-contrib-stylus --save-dev
	npm install grunt-contrib-uglify --save-dev
	npm install grunt-contrib-watch --save-dev

创建 `grunt` 配置文件 `Gruntfile.js`

	module.exports = function(grunt) {
		grunt.initConfig({
			pkg: grunt.file.readJSON('package.json'),
			dir: {
				ext: 'typo3conf/ext/*/',
				source: 'Resources/Private/',
				build: 'Resources/Public/',
				css: {
					path: 'Stylus/',
					src: '*.styl',
				},
				js: {
					path: 'Javascript/',
					src: '*.js',
				},
			},
			stylus: {
				compile: {
					files: grunt.file.expand('typo3conf/ext/*/').map(function(extPath) {
						return {
							expand: true,
							cwd: extPath + '<%= dir.source %><%= dir.css.path %>',
							src: '<%= dir.css.src %>',
							dest: extPath + '<%= dir.build %>Stylesheets/',
							ext: '.css',
						};
					}),
				}
			},
			uglify: {
				options: {
					mangle: true,
					compress:true,
					preserveComments: 'all',
				},
				build: {
					files: grunt.file.expand('typo3conf/ext/*/').map(function(extPath) {
						return {
							expand: true,
							cwd: extPath + '<%= dir.source %><%= dir.js.path %>',
							src: '<%= dir.js.src %>',
							dest: extPath + '<%= dir.build %>Javascript/',
							ext: '.js',
						};
					}),
				}
			},
			watch: {
				options: {
					interrupt: true,
					livereload: true,
				},
				css: {
					files: '<%= dir.ext %><%= dir.source %><%= dir.css.path %><%= dir.css.src %>',
					tasks: 'stylus',
				},
				js: {
					files: '<%= dir.ext %><%= dir.source %><%= dir.js.path %><%= dir.js.src %>',
					tasks: 'uglify',
				},
			},
		});
		grunt.loadNpmTasks('grunt-contrib-stylus');
		grunt.loadNpmTasks('grunt-contrib-uglify');
		grunt.loadNpmTasks('grunt-contrib-watch');
		grunt.registerTask('default', ['watch']);
	};

每次开发时，以命令行模式运行 `grunt`

[>> 返回](./README.md)