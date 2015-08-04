# grunt-tutorial
A set of demo files for Grunt tutorial

npm init

# Open the package.json file and add the dependencies

{
	"name": "my-project",
	"version": "0.1.0",
	"devDependencies": {
		"grunt": "~0.4.5",
		"grunt-contrib-jshint": "~0.10.0",
		"grunt-contrib-concat": "~0.4.0",
		"grunt-contrib-uglify": "~0.5.0",
		"grunt-shell": "~0.7.0"
	}
}

# To install Grunt and the modules specified in the file

npm install --save-dev

# Do a quick version check

grunt --version

# If grunt --version throws up an error, it means Grunt wasn't installed properly.
# To reinstall Grunt, enter the following commands in the terminal:

rm –rf node_modules
npm cache clean
npm install

vi gruntfile.json

module.exports = function(grunt) {
	// Project configuration.
	grunt.initConfig({
		jshint:{
			all:['scripts.js', 'scripts1.js','scripts2.js']
		},
		concat: {
			dist: {
				src: ['scripts.js', 'scripts1.js','scripts2.js'],
				dest: 'merged.js'
			}
		},
		uglify: {
			dist: {
				src: 'merged.js',
				dest: 'build/merged.min.js'
			}
		},
		cssmin: {
			options: {
				shorthandCompacting: false,
				roundingPrecision: -1
			},
			target: {
				files: {
				'css/output.css': ['css/foo.css', 'css/bar.css']
				}
			}
		},
		cssmin: {
			target: {
				files: [{
					expand: true,
					cwd: 'release/css',
					src: ['*.css', '!*.min.css'],
					dest: 'release/css',
					ext: '.min.css'
				}]
			}
		},
		shell: {
			multiple: {
				command: [
					'rm -rf merged.js',
					'mkdir deploy',
					'mv build/merged.min.js deploy/merged.min.js'
				].join('&&')
			}
		}
	});

	grunt.loadNpmTasks('grunt-contrib-jshint');
	grunt.loadNpmTasks('grunt-contrib-concat');
	grunt.loadNpmTasks('grunt-contrib-uglify');
	grunt.loadNpmTasks('grunt-contrib-csslint');
	grunt.loadNpmTasks('grunt-contrib-cssmin');
	grunt.loadNpmTasks('grunt-shell');

	// Default task.
	grunt.registerTask('default', ['jshint','concat','uglify','shell']);
};
