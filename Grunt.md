# Ubuntu 20.04♥中的TYPO3 —— Node.js

借助Grunt及相关插件对图片、.html、.css和.js进行相应的管理。

从[Node.js官网](https://nodejs.org/)下载Node.js并安装，Grunt详细安装步骤请参考 [这里](https://gruntjs.com/getting-started)

*以下操作步骤在开发目录下进行*

以命令行模式运行 `npm install`，根据提示创建 `package.json`

    {
        "description": "Project description here...",
        "license": "GPL-2.0"
        "README": "",
        "repository": {},
    }

全局安装`grunt-cli`，如果已经安装，请跳过此步

    npm install -g grunt-cli

安装`grunt` 并保存至 `package.json` 中

    npm install grunt --save-dev

安装HTML（以`grunt-contrib-htmlmin`为例）、图片（以`grunt-contrib-imagemin`为例）、css（以 `grunt-contrib-stylus` 为例）、js（以 `grunt-contrib-uglify` 为例）、任务监控（以 `grunt-contrib-watch`为例）相关插件，并保存至 `package.json` 中

    npm install grunt-contrib-htmlmin --save-dev
    npm install grunt-contrib-imagemin --save-dev
    npm install grunt-contrib-stylus --save-dev
    npm install grunt-contrib-uglify --save-dev
    npm install grunt-contrib-watch --save-dev

创建 `grunt` 配置文件 `Gruntfile.js`

    module.exports = function(grunt) {
        grunt.initConfig({
            pkg: grunt.file.readJSON('package.json'),
            dir: {
                base: 'typo3conf/ext/*/',
                source: 'Resources/Private/',
                build: 'Resources/Public/',
                html: {
                    path: 'Html/',
                    src: '**/*.html',
                },
                image: {
                    path: 'Image/',
                    src: '**/*.{gif,jpeg,jpg,png,svg}',
                },
                css: {
                    path: 'Stylus/',
                    src: '**/*.styl',
                },
                js: {
                    path: 'Javascript/',
                    src: '**/*.js',
                },
            },
            htmlmin: {
                options: {
                    caseSensitive: true,
                    collapseWhitespace: true,
                    keepClosingSlash: true,
                    removeComments: true,
                },
                compress: {
                    files: grunt.file.expand('typo3conf/ext/*/').map(function(extPath) {
                        return {
                            expand: true,
                            cwd: extPath + '<%= dir.source %><%= dir.html.path %>',
                            src: '<%= dir.html.src %>',
                            dest: extPath + '<%= dir.source %>',
                            ext: '.html',
                            extDot: 'last',
                            flatten: false,
                        };
                    }),
                },
            },
            imagemin: {
                compress: {
                    files: grunt.file.expand('typo3conf/ext/*/').map(function(extPath) {
                        return {
                            expand: true,
                            cwd: extPath + '<%= dir.source %><%= dir.image.path %>',
                            src: '<%= dir.image.src %>',
                            dest: extPath + '<%= dir.build %>Images/',
                            extDot: 'last',
                            flatten: false,
                        };
                    }),
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
                            extDot: 'last',
                            flatten: false,
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
                            extDot: 'last',
                            flatten: false,
                        };
                    }),
                }
            },
            watch: {
                options: {
                    interrupt: true,
                    livereload: true,
                },
                config: {
                    files: 'Gruntfile.js',
                },
                html: {
                    files: '<%= dir.base %><%= dir.source %><%= dir.html.path %><%= dir.html.src %>',
                    tasks: 'htmlmin',
                },
                image: {
                    files: '<%= dir.base %><%= dir.source %><%= dir.image.path %><%= dir.image.src %>',
                    tasks: 'imagemin',
                },
                css: {
                    files: '<%= dir.base %><%= dir.source %><%= dir.css.path %><%= dir.css.src %>',
                    tasks: 'stylus',
                },
                js: {
                    files: '<%= dir.base %><%= dir.source %><%= dir.js.path %><%= dir.js.src %>',
                    tasks: 'uglify',
                },
            },
        });
        grunt.loadNpmTasks('grunt-contrib-htmlmin');
        grunt.loadNpmTasks('grunt-contrib-imagemin');
        grunt.loadNpmTasks('grunt-contrib-stylus');
        grunt.loadNpmTasks('grunt-contrib-uglify');
        grunt.loadNpmTasks('grunt-contrib-watch');
        grunt.registerTask('default', ['watch']);
    };

每次开发时，以命令行模式运行 `grunt`

[<< 返回](README.md)