# Note
Latest version is available in `compatible_with_neovim_master` branch,
it's compatible with master branch of neovim and requires features introduced
in that branch. `master` branch is frozen until neovim releases those features
and work is done on `compatible_with_neovim_master`.

# What's qnvim
qnvim helps those who are used to editing text in vim and also need Qt Creator features to combine these two.

It runs an instance of Neovim inside Qt Creator, so it's able to run your `init.vim` and all your vim plugins and your tweaks in `init.vim` should work.

<p align="center">
  <a href="https://www.youtube.com/watch?v=twwnnduujzw">
    <img src="https://user-images.githubusercontent.com/1270688/51085365-02e51900-174d-11e9-92f7-c6daa5ec33de.gif"/>
  </a>
</p>

# Status
It's in beta but it's mostly stable and usable, for last few months I've been using Qt Creator only with this plugin with no pain. Currently these are the known issues:
1. It can't show some special buffers (buffer types like quickfix, special buffers some plugins create, etc, plugins such as gundo, tagbar, gitgutter, etc)
2. `wrap` doesn't work alright (just a minor display problem, it's due to lake of a feature in neovim, described in this issue: https://github.com/neovim/neovim/issues/8037).

All my 149 plugins installed in neovim work alright except a few that relate on highlights (Qt Creator highlights C++ and QML better than any vim plugin, so it's totally alright.) and those that rely on special buffers. (Work is in progress to handle all types of buffers.)

Please let me know if you find any problems and please contribute to this project if you have the time.

# Install Instructions
1. Build Qt Creator from git repository (https://wiki.qt.io/Building_Qt_Creator_from_Git)

If you build the head of master branch, then you can use qnvim only with your build, if you wanna use qnvim with the official release of Qt Creator you should checkout the tag that matches your installed Qt Creator.

2. Clone and compile https://github.com/equalsraf/neovim-qt
3. Install devel package of msgpack.
4. Open the `qnvim.pro` file as a project in your offical Qt Creator (not the one you built.)
5. Setup locations to Qt Creator build and neovim-qt in `qnvim.pro` file.
Like this:
```
isEmpty(IDE_SOURCE_TREE): IDE_SOURCE_TREE = "<PATH_TO_QT_CREATOR_CLONED_REPO>"
isEmpty(IDE_BUILD_TREE): IDE_BUILD_TREE = "<PATH_TO_QT_CREATOR_BUILD_DIRECTORY>"
INCLUDEPATH += <PATH_TO_NEOVIM_QT_SRC_DIRECTORY> <PATH_TO_MSGPACK_HEADERS>
LIBS += -L<PATH_TO_NEOVIM_QT_LIB_DIRECTORY> -lneovim-qt -lneovim-qt-gui -L<PATH_TO_MSG_PACK_LIB_DIRECTORY> -lmsgpackc
```
For example:
```
isEmpty(IDE_SOURCE_TREE): IDE_SOURCE_TREE = "/home_direcotry/packages/qt-creator"
isEmpty(IDE_BUILD_TREE): IDE_BUILD_TREE = "/home_direcotry/packages/qt-creator-build"
INCLUDEPATH += /home_direcotry/packages/neovim-qt/src /usr/local/Cellar/msgpack/2.1.5/include
LIBS += -L/home_direcotry/packages/neovim-qt/build/lib -lneovim-qt -lneovim-qt-gui -L/usr/local/Cellar/msgpack/2.1.5/lib -lmsgpackc
```

6. Setup locations to your Qt Creator build in Projects tab.
In the Qt Creator go to `Projects` Tab/Mode (you can select it in the left column) Active project should be `qnvim`, and in Build & Run `Desktop ...` should be selected. Under `Desktop ...` select `Run` and in the right side in the `Run` section set Executable to `<full path to>/qt-creator-build/bin/qtcreator` and working directory to `<full path to>/qt-creator-build/bin`

7. Build and run the project.

8. Put the built library in the location that Qt Creator expects plugins (it varies based on your OS) and use the built Qt Creator instead of the official version. (Or if you checked out the tag that corresponds to your installed Qt Creator, then you can use your own installed Qt Creator.)

# Sample `.qnvimrc`
There's a sample `.qnvimrc` file available in the repo, it provides most of the convenient keyboard shortcuts for building, deplying, running, switching buffers, switching tabs, etc. It'll also help you understand how you can create new keyboard shortcuts using Qt Creator commands.

# Credits

## Neovim
The lovely text editor that solves the problem of writing AND editing text once for ever.

https://neovim.io
https://github.com/neovim/neovim

## Qt
The lovely cross platform framework that lets you build awesome software with its full stack of tools from networking to ui controls to 2d/3d graphics and many others.

https://www.qt.io

## Qt Creator
The lovely IDE that lets you use the full power of Qt in an user friendly environemnt (I rememeber days that Qt Creator didn't exist and to code with Qt you had to use Eclipse or bare terminal and it was like a nightmare, Qt Creator eased the programming with Qt a lot.)

https://www.qt.io/qt-features-libraries-apis-tools-and-ide/#ide

https://en.wikipedia.org/wiki/Qt_Creator


## Neovim Qt
The C++ binding for neovim's msgpack communication layer.

https://github.com/equalsraf/neovim-qt

#### And lots of other libraries that are used in above projects and are mentioned in their docs
