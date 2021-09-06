## pnpm: Javascript New Package Manager

`pnpm` is also known as `performent npm`. It is a new package manger which can be used instead of `npm` or `yarn`. It is basically a drop-in replacement for `npm`, which means that once you install it, you can invoke `pnpm install` to download a project dependencies, and all will work transparently for you.

What differentiates `pnpm` is the way packages are managed. npm and Yarn install separate copies of the packages in every project, on the other hand, pnpm keeps a single copy of every package and uses hard links/symlinks to reference the original installation. So:
- if you depend on different versions of the dependency, only the files that differ are added to the store. For instance, if it has 100 files, and a new version has a change in only one of those files, `pnpm update` will only add 1 new file to the store, instead of cloning the entire dependency just for the singular change.
- All the files are saved in a single place on the disk. When packages are installed, their files are hard-linked from that single place, consuming no additional disk space. This allows you to share dependencies of the same version across projects.

real-world example:
```
**npm:**
Project Size: 1.5 GB

**pnpm:**
Project Size: 228 MB //reduce the space up to 85%
```
The above illustration has been tested in my real project. 

all in all, you save a lot of space on your disk, and your installations would be twice faster than other package managers!

Installation:   [click here for more information about installation](https://github.com/pnpm/pnpm#installation) 
