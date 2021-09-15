## How to install Figma on Linux

[Figma](https://www.figma.com/) is a great UI/UX tool with a quite generous free tier. This means many developers use Figma to prototype their application or website designs (including me). Many of us developers tend to use Linux but that is where a problem arises, the Figma app is not available for Linux!!!

Now, to be fair, Figma has a web version which is almost exactly what the desktop version is but the desktop version is still preferred by most. 

# How do we get the Figma app on Linux?
Well, a great developer thought of solving this issue by making an unofficial version of Figma for Linux and the best part is that it is open source. See the GitHub Repository [here](https://github.com/Figma-Linux/figma-linux). The app is extremely similar to the Windows version of Figma. 

# How is the desktop app different from the web version?
The desktop app is built on electron (both, the official version for Windows and macOS as well as the unofficial version for Linux). The main advantages are better font support, in-app tabs (which is extremely useful for me), and extension development.

# One Small Problem which can be fixed
When you are installing Figma Linux on Ubuntu, you might use the PPA repository way. This way seems to have issues and Figma won't launch. If you ever try to launch it from the terminal, you will see this error -
```text
figma-linux: error while loading shared libraries: libffmpeg.so: cannot open shared object file: No such file or directory
```
So what is the fix? 
Don't use the PPA!!!
Get the `.deb` package from the [releases page](https://github.com/Figma-Linux/figma-linux/releases)
If you have already downloaded from the PPA, you can simply overwrite it by installing the .deb (It might ask you to downgrade, doing that will also work). We also need to hold it off `apt upgrade` or else it will automatically update and cause the issue again.

To do this run the following command - 
```bash
sudo apt-mark hold figma-linux
```

And that is it!!! The issue is fixed and I hope Figma Linux works well for you. If you have any doubts, you can leave down a comment below. For bugs, submit a GitHub issue [here](https://github.com/Figma-Linux/figma-linux/issues)

