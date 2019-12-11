I've been using Netlify for quite a while already. I use netlify to host both [https://taskifyio.netlify.com/](https://taskifyio.netlify.com/) and [https://billjellesmacoding.netlify.com/](https://billjellesmacoding.netlify.com/), the blog that you're reading this article on right now. With just the hosting alone, I love using Netlify as it was an extremely easy and quick way (and free) for me to get my projects up and running on the web. However, I know that Netlify has loads of other really cool features that I wasn't taking advantage of so I decided to do some explorering.

# What is Netlify

Netlify is a platform for hosting your front end application. I say frontend here because if you need to host more backend features for your app such as an api or database, you may need to find additional products. You can still use Netlify to host your frontend, which is very valueable in this day and age given the explosion of javascript frameworks and static site generators.

For example, my blog is built using GatsbyJS, a static site generator. Essentially, once I'm ready to deploy a new version of my blog, I run the `gatsby build` command and serveral html, css, and javascript files are spit into my public folder. These files don't need a fancy interpretter and just need to be viewed in a modern web browser. All I need is simply web hosting for those files. This makes Netlify the perfect all in one solution. Even my blog posts, which I write in markdown, are able to be built into html files. 

My taskify app is a little bit more complicated. I use `Vue.JS` for the frontend so Netlify has no trouble hosting this. I have a Flask based backend api running on a different port for retreiving my lists and tasks. Netlify is unable to host a Flask application so I need to use Heroku. Taskify also uses a database for storing the lists and tasks. Again, I need to look elsewhere for my database and use a cloud based MongoDB.

* You can get a free subdomain or buy your own domain

As of now, I'm using a free subdomain which is why the webaddress of this blog has a `.netlify.com` rather than just a `.com`. I could go out and buy a domain from GoDaddy or some other domain registrar. I would then simply use the name servers that netlify gives me. 

* Deploys straight from Github

You're able to set Netlify up to build straight from a github code repository. This is great because I simply commit my code and push it to Github when I'm finished and Netlify takes it from here. You will want to tell Netlify which folder to use as the foot of your website, this is specified in a `netlify.toml` file which you will put in the root of your project. In my case, Gatsby will build all of my files to a `/public` folder so I simply specify what's being published under the build command of the `netlfiy.toml` file.

```toml
[build]
    publish="public"
```

# Built in Security

Netlify understands the importance of security and offers **free** HTTPS on all of their hosted websites. Https is incredibly important for any web app/site that has forms and logins. Https encrypts communication so when you're entering sensative information into forms, you definetly want encryption so that the bad guys can't get a hold of your credentials. Google has also taken a notice of the importance of HTTPS in today's increasingly online world. Therefore, Google makes known that one aspect of how they rank websites in their search results is by giving higher weight to websites that have HTTPS. HTTPS has long been known to have these capabilities, but it has also been known to be confusing and costly to enable HTTPS. Netlify makes this process easier by offering free HTTPS.


