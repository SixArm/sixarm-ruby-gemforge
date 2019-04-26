# SixArm.com → Ruby → <br> Gem tools for building our own gems

* Doc: <http://sixarm.com/sixarm_ruby_gemforge>
* Gem: <http://rubygems.org/gems/sixarm_ruby_>
* Repo: <http://github.com/sixarm/sixarm_ruby_gemforge>
<!--header-shut-->


## Introduction

These require scripts in sixarm_ruby_gem_scripts.

You can customize these however you like for your own systems.

For docs go to <http://sixarm.com/sixarm_ruby_gemforge>

Want to help? We're happy to get pull requests.

## Examples

To find directories that contain typical gemspec files:

    find */*gemspec -exec dirname {} \;

To change into each directory, then run a command, such as echo:

    find */*gemspec -exec dirname {} \; |
    while read dir; do
      pushd $dir > /dev/null
      echo "=== $dir ==="
      popd > /dev/null
    done

To update each directory:

    find */*gemspec -exec dirname {} \; |
    while read dir; do
      pushd $dir > /dev/null
      echo "=== $dir ==="
      git pull --rebase=preserve
      git push
      popd > /dev/null
    done

To update the README and publish it:

    find */*gemspec -exec dirname {} \; | 
    while read dir; do
      pushd $dir > /dev/null
      git pull --rebase=preserve
      gemforge-update-readme
      git add README.md
      git commit -m "Update README"
      git push
      echo "The script is in $dir"
      popd > /dev/null
    done
