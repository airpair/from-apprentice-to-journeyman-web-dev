This article is intended for people who have some knowledge of programming and would like to program web applications more efficiently. I'll show you how to most quickly integrate open source projects via the command line, and a few other best practices for development.

 > I recently realized that I'm no longer a timid developer. I realized the tools I use are so much better than how I originally handled minor issues. Most of the skills I have now that make me a great developer are not how well I can write AngularJS code, but the things I use *while* I develop. The end product is usually better as a result, but I want to draw attention to the development workflow, especially for new developers.
 
## Install jQuery the right way!
 
Pretend you want to use jQuery. A new developer might google [jquery](https://jquery.com/download/) and download the `.js` files via the links they find on the first google hit. Done. You can now use jQuery. But think about this and be as pessimistic as possible: you realized you need to use jquery in the project, so you stop. At this point, the clock is ticking. You google jquery, you find the package. You download it, you move it into your project. That's too many steps. That could take 5 minutes or more. How can we improve this process?

The answer is Node. Don't leave! This article is not about Node. Node comes with a command line interface (CLI) called Node Package Manager (NPM). I highly reccomend you use NPM as often as possible. Here are some of the benefits of using NPM.

 * Setting up NPM is a one-time hassle, which will forever increase your productivity
 * Using NPM to install open source projects will save you time
 * You will become someone who browses npmjs.org, and be exposed to things you may never have been exposed to before

Use NPM. NPM is your friend. Most everything is available via NPM. Here's what you would do to add jquery to your project, via NPM: `npm install jquery --save-dev`. What happens next is a node_modules folder will be created, with a jquery folder beneath that. You don't have to move your downloaded jquery file from your downloads folder to your project, node will automatically organize these external files - these packages - into a node_modules folder. 

Once you completely switch to using NPM for all external packages, you will notice your applications architecture has improved. You will also, if you use the optional `--save-dev` flag, be able to include these dependencies, without including every file associated with those dependencies. Every time you use --save-dev, the package installed (e.g. jQuery) will be added to a **package.json** file. You've probably seen package.json in some github projects. What this package.json file does, is when you download (or git clone) a project that has a package.json, you can simply run `npm install` and NPM will parse the package.json file and install all packages into node_modules. This way you can commit your project to git (your project uses jQuery), without including your own file of jQuery.


## Download Twitter Bootstrap Hassle-Free!
 
 Your jQuery project has progressed and now you need to use bootstraps button classes, the grid, and other things in bootstrap. Now that we are using NPM for everything, we think let's install that package with NPM. So, you don't know if it's bootstrap, twitter-bootstrap, but a quick google of *"npm install bootstrap"* will help us know what the package is called on the node package network. We see it is simply called bootstrap and we run `npm install bootstrap`

It might be subtle, but for a project that uses jQuery and Bootstrap, we could save upwards of half an hour installing these two packages via NPM. You avoid navigating through the project's documentation, you avoid deciding which parts of the package you do or don't need, and you avoid your web browser all together (therefore, you aren't at risk to absent mindedly open a new tab and browse reddit). Think about how this scales: you might eventually have a project that has tens of open source packages. You would not want to spend a whole day finding each of the packages downloadable zip file, extracting them, figuring out which files you need and how to organize them.
 
## Host your LIVE DEMO for FREE at GH-PAGES!
 
 This section will include a tutorial of how I created [my markdown editor](http://juliusakula.github.io/editor/#/) and hosted it through github-pages. 
 
 > The most important things to know, are the things that you don't know that you don't know them. It's so much easier to learn something if you are aware that you need to learn it. And if you don't know what you need to learn, you don't even know what to google to find out about it.
 
 Github pages a.k.a. how to get the most out of github. Did you know, that you can have a website hosted for free through github? It's very simple, and for some reason it seems like a secret-feature of github. Since I found out about github-pages, I have not worried about being skilled enough to contribute to open-source projects. I know that if I want to pad my resume with open source contributions, a simple task that most projects could benefit from is a good gh-pages demo. If it is hosted on github, it might as well have a gh-pages demo.
 
 Take for example, my markdown editor project. My github username is *juliusakula*. The project name is *editor*. The source code can thus be found at https://github.com/juliusakula/editor/. When this project is hosted on gh-pages, the URL is similar but somewhat different: http://juliusakula.github.io/editor/.
 
 I said using gh-pages was simple. Normally, you will run the command `git push origin master` -- this pushes your local master branch changes to the remote repository master branch. To make github host the project, run the command `git push origin master:gh-pages`. This pushes your local master branch to the remote's gh-pages branch. Within a couple of minutes, you will be able to see your project live, hosted for free. After the first push to remote gh-pages, subsequent pushed changes will be visible nearly instantly. In the settings of the github repo you can find the gh-pages link (or, rearrange the project name and github user as I described in the paragraph above), you want to include that link in the projects main README.md file so that people going to your repository know that a demo is available.
 
## Let's make a project from scratch, like a boss!
 
 I wanted a tool that I could type Markdown in one place, and see it render in another. I know angularJS and I wanted to use a markdown directive. I knew this problem had been solved before, so I searched for markdown directives, and I found [angular-md](https://www.npmjs.com/package/angular-md). This page does have a demo, but I didn't like it. I like bootstrap. I also wanted to use angular directives, because it's the one part of angular that I still have tons of hours of learning yet to do.
 
 So I identified several packages that I would need. It is possible to chain `npm install` together, so I installed all these packages with one command
 
 `npm install bootstrap angular angular-ui-bootstrap angular-ui-router angular-md marked ng-clip zeroclipboard --save-dev`
 
 That will fetch all the files I need, and neatly organize them into the node_modules folder. Let's create app.js and index.html and look at the organization of the project thus far:
 
 ```
editor/
  |- node_modules/
  |  |- bootstrap/
  |  |- angular/
  |  |- angular-ui-bootstrap/
  |  |- angular-ui-router/
  |  |- angular-md/
  |  |- marked/
  |  |- ng-clip/
  |  |- zeroclipboard/
  |- app.js
  |- index.html
  |- package.json
```
 Mind you, this is 30 seconds into a project and we already have all the dependencies installed. Now, we create our angular project in app.js, and work on index.html until we are satisfied. I will not go into detail on the work done in angular for this project, I'd like this to focus on the workflow of getting a demo up on gh-pages.
 
 Your `index.html` file will have certain references to files that you **do** want to commit and push to github, however you do not want to commit your entire node_modules folder to github (use the `--save-dev` flag instead, and commit your package.json). Once you add all files that are referenced (see my markdown project's [index.html](https://github.com/juliusakula/editor/edit/master/index.html) file, all items in `<link>` and `<script>` tags are included in the git commit), push those files to the remote gh-pages branch. Then visit your demo page and add the link to the main README.md file. 
 
 Just like that, you have a project that has a live demo. You installed your packages the lazy way, and have a package.json file to prove it. New developers will benefit greatly by showcasing a project hosted on github. It proves you use version control, it proves you've ever worked on coding at all. It proves you can find the most cost effective way to host a demo, and therefore aren't likely to waste company money. Github projects are a radiant gold star on resumes, and having a live demo will greatly improve the chances people will understand what the project actually *does*.