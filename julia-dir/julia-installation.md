# Julia Installation 

## Introduction
[Julia](https://julialang.org) is a dynamically typed compiled programming language developed at [MIT](https://julia.mit.edu) for general purpose computing. [Julia](https://julialang.org) has a number of interesting features, and is [an open source project available under the MIT license](https://github.com/JuliaLang/julia). [Julia](https://julialang.org) is available on all major computing platforms and operating sytstems (macOS, Windows and Linux). In addition, in this course we'll be using [Visual Studio Code (VS Code)](https://code.visualstudio.com) to compose and run our [Julia](https://julialang.org) programs.

In this chapter, we will:
* Discuss the {ref}`content:references:julia-installation`
* Discuss the {ref}`content:references:vscode-installation`

---

(content:references:julia-installation)=
### Installation and Requirments for Julia
[Julia](https://julialang.org), which runs on all major systems, can be downloaded from the [Julia downloads page](https://julialang.org/downloads/). Select the appropriate download version, and then follow the instructions for installation. 

For Windows users, before downloading [Julia](https://julialang.org), please see the specific instructions below.

### macOS
On macOS, a ``julia-1.x.x-mac64.dmg`` installation file is contained in the download, which contains the executable ``Julia-1.x.app``. Installation of [Julia](https://julialang.org) on macOS works the same as any other Mac software: drag the Julia-1.x.app to Applications Folder. [Julia](https://julialang.org) runs on macOS 10.9 Mavericks or later.

To launch [Julia](https://julialang.org) from the command line, you'll need to update your ``PATH`` environmental variable to include the location of [Julia](https://julialang.org); add the following line to the ``.zshrc`` file in your home directory using the [nano text editor](https://www.nano-editor.org) or some other editor (path on macOS for version `1.7`, your path may be different):

```zsh
export PATH="$PATH:/Applications/Julia-1.7.app/Contents/Resources/julia/bin"
```

Alternatively, you can create a [symlink](https://en.wikipedia.org/wiki/Symbolic_link) to a [Julia](https://julialang.org) version of your choosing by executing the following commands in the [Terminal on macOS](https://support.apple.com/guide/terminal/open-or-quit-terminal-apd5265185d-f365-44cb-8b09-71a064a42125/mac):

```zsh
sudo mkdir -p /usr/local/bin
sudo rm -f /usr/local/bin/julia
sudo ln -s /Applications/Julia-1.7.app/Contents/Resources/julia/bin/julia /usr/local/bin/julia
```

### Linux and FreeBSD
The official generic binaries from the downloads page can be used to install [Julia](https://julialang.org) on Linux and FreeBSD. The following set of commands downloads the latest version of Julia into a directory named ``julia-1.7.3``:

```bash
wget https://julialang-s3.julialang.org/bin/linux/x64/1.7/julia-1.7.3-linux-x86_64.tar.gz
tar zxvf julia-1.7.3-linux-x86_64.tar.gz
```

The generic Linux and FreeBSD binaries do not require any special installation steps. Thus, once [Julia](https://julialang.org) has been downloaded and unpackaged, it can be moved to wherever you wish. 

However, to start [Julia](https://julialang.org) you'll need to update your ``PATH`` environmental variable to point the installation location. Add the following line the `.bashrc` file in your home directory:

```bash
export PATH="$PATH:/path/to/<Julia directory>/bin"
```

### Windows
Although [Julia](https://julialang.org) can run on Windows directly, the teaching team asks that all Windows users install [the Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/about), along with the latest [Ubuntu](https://ubuntu.com) distribution, to run [Julia](https://julialang.org) in a Linux environment.  Instructions on how to install WSL can be found [here](https://docs.microsoft.com/en-us/windows/wsl/install).

Once [the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about) has been installed, [Julia](https://julialang.org) can installed following the [Generic Linux instructions](https://julialang.org/downloads/platform/#linux_and_freebsd).

(content:references:vscode-installation)=
### Installation and Requirments for VSCode
[Visual Studio Code (VSCode)](https://code.visualstudio.com) is a source-code editor made by [Microsoft](https://www.microsoft.com/en-us/?ql=4) for Windows, Linux, and macOS. VSCode supports debugging, syntax highlighting, intelligent code completion, snippets, and code refactoring for various programming languages, including [Julia](https://julialang.org).

To install VSCode, go to the [Visual Studio Code](https://code.visualstudio.com) homepage and click on the download button ({numref}`fig-vscode-download`):


```{figure} ./figs/Fig-vscode-download.png
---
height: 460px
name: fig-vscode-download
---
To download Visual Studio Code, click on the download button and follow the on-screen instructions.
```

Once VSCode has been installed, we need to install the [Julia extension for VSCode](https://code.visualstudio.com/docs/languages/julia). The [Julia extension for VSCode](https://code.visualstudio.com/docs/languages/julia) enables syntax highligting, access to a modern debugger, built-in dynamic autocompletion, inline results, plot pane, integrated REPL, variable view, code navigation, and many other advanced language features.

To install the [Julia extension for VSCode](https://code.visualstudio.com/docs/languages/julia), open VSCode and navigate to the [extensions panel](https://code.visualstudio.com/docs/editor/extension-marketplace). In the search field, enter `Julia` and select the green install button on the `Julia language support` extension ({numref}`fig-vscode-julia-ext`):

```{figure} ./figs/Fig-vscode-julia-ext.png
---
height: 460px
name: fig-vscode-julia-ext
---
The [Julia extension for VSCode](https://code.visualstudio.com/docs/languages/julia) can be installed from the Extension tab of [Visual Studio Code (VSCode)](https://code.visualstudio.com) or by accessing the Extensions from the Preferences menu.
```

---

## Additional Resources
* For the latest information on [Julia](https://julialang.org), check out the [Julia blog](https://julialang.org/blog/).
* For the latest updates on [VSCode](https://code.visualstudio.com), check out the [VSCode blog](https://code.visualstudio.com/blogs/2022/08/16/markdown-language-server).