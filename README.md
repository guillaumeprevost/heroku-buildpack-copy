# heroku-buildpack-subdir-copy

Add as a first buildpack in the chain. Set `PROJECT_PATH` environment variable to point to project root. It will be promoted to slug's root, everything else will be erased. Following buildpack (e.g. nodejs) will finish slug compilation.

**Disclaimer:** The code may change without notice, so always pin to specific github version. Provided as is.

## How to use

1. `heroku buildpacks:clear` if necessary
2. `heroku buildpacks:set https://github.com/guillaumeprevost/subdir-heroku-buildpack`
3. `heroku buildpacks:add heroku/nodejs` or whatever buildpack you need for your application
4. `heroku config:set PROJECT_PATH=projects/nodejs/frontend` pointing to what you want to be a project root.
5. Deploy your project to Heroku.

## Optional : copying files & folders before erasing root

You can add a file name `Copyfile` to your codebase root listing all the files and folders you need to copy inside the subdir specified in PROJECT_PATH.

Files and folders listed there will be copied inside the sub-directory BEFORE erasing everything else.

## How it works

The buildpack takes subdirectory you configured, optionally copies files and folders specified in Copyfile to the subdirectory, erases everything else, and finally copies that subdirectory to project root. Then normal Heroku slug compilation proceeds.

## Credits

Inspired by :

- [https://github.com/timanovsky/subdir-heroku-buildpack](https://github.com/timanovsky/subdir-heroku-buildpack)
- [https://github.com/calvingiles/heroku-buildpack-copy](https://github.com/calvingiles/heroku-buildpack-copy)
