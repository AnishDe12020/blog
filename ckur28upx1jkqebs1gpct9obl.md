## The Joy of Contributing to Open Source

Back in July of this year, I made a bold decision of completely switching to Pop OS (an ubuntu-based Linux distribution) and I was faced with many hurdles. One of these was an alternative to [Microsoft's Your Phone application](https://www.microsoft.com/en-us/p/your-phone/9nmpj99vjbwv?activetab=pivot:overviewtab). 

After some research, I stumbled over an application called [KDE Connect](https://kdeconnect.kde.org/) which turned out to be a great alternative as it not only did everything that Microsoft's Your Phone application did but had some more nifty features.

# My first pull request
As Pop OS uses Cosmic (a fork of the popular GNOME desktop environment), I was better off using [GSConnect](https://extensions.gnome.org/extension/1319/gsconnect/) instead of the native KDE Connect application. GSConnect is a fork of KDE Connect which integrates well with GNOME. Everything was good until I discovered a feature that allowed me to share the URL of my current tab to my phone. This needed me to download the [GSConnect chrome extension](https://chrome.google.com/webstore/detail/gsconnect/jfnifeihccihocjbfcfhicmmgpjicaec) but I use Microsoft Edge as my primary web browser. Now, chrome extensions work on Microsoft Edge as it is chromium-based but the GSConnect chrome extension made use of a feature called [native messaging](https://developer.chrome.com/docs/apps/nativeMessaging/) which helped the browser extension and a program installed on the computer interact with each other. Sadly, this needs dedicated configuration for each browser (it is just a line of code). GSConnect didn't have support for Microsoft Edge at that time and hence I decided to [open an issue](https://github.com/GSConnect/gnome-shell-extension-gsconnect/issues/1139).

A collaborator got back to me and explained the issue to me. I was a bit stuck and so asked for more help on GitHub and the same person got back to me, giving me a place to start working on the issue. I quickly figured out the problem and fixed the issue on my end. The next step was to open a pull request so I cloned the repository, made the changes, pushed the code, and opened [my first ever pull request](https://github.com/GSConnect/gnome-shell-extension-gsconnect/pull/1141). I did mess up with the code style because I had forgotten to read the contributing guide and hence didn't run the linter checks. Anyways, a member got back to me and I fixed the problem and then my pull request was merged 🎉.

## The joy when my pull request got merged
As soon as I saw the notification that my pull request had been merged, I felt the joy of contributing to an application used by many people. This is the moment you realize that you are not working for nothing, you are getting happiness from helping others and you are learning a lot yourself. Contributing to open-source also adds to your portfolio, it shows that you care about the project.

## The learning
When I opened the issue, I didn't know anything about native messaging in chrome extensions but from discovering this bug to fixing it, I learned a lot about how native messaging works and how open-source contributions work.

I have talked about the perks of contributing to open-source in [my last article](https://blog.anishde.dev/open-source-in-everyday-life).

# Getting Started with contributing to open-source
It is not hard to experience the joy of contributing to open-source. Look for issues that you might want to work on and if you find one which you want to work on, it is as simple as making the changes and opening a pull request (make sure to follow the repository's contributing guide if it has one). Also, check out [Hacktoberfest](https://hacktoberfest.digitalocean.com/) where you open 4 **valid** pull requests on participating repositories and if you are the first 50k to do so, you get some swag. Do check out [this guide on getting started with Hacktoberfest](https://ayushirawat.com/beginners-guide-to-hacktoberfest-2021) by @[Ayushi Rawat](@ayushi7rawat) if you feel stuck.

Feel free to comment down if you feel like I missed something or you got a question. You can also reach out to me on [Twitter](https://twitter.com/AnishDe12020).

Happy contributing :D

