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

# Forms

One cool feature that I decided to explore a little bit more was form submission. I could create a contact form for comments on the blog or a signup form for a newsletter. Adding a form can be a little bit more difficult than it may seem in the docs. In the admin dashboard for my blog, I clicked the forms tab and it gave me this little snippit of code to put on a page.

```html
<form name="contact" netlify>
  <p>
    <label>Name <input type="text" name="name" /></label>
  </p>
  <p>
    <label>Email <input type="email" name="email" /></label>
  </p>
  <p>
    <button type="submit">Send</button>
  </p>
</form>
```

Unfortunately, I found that I needed instead to use the sample code in the official docs:

```html
<form name="contact" method="POST" data-netlify="true">
    
  <p>
    <label>Your Name: <input type="text" name="name" /></label>   
  </p>
  <p>
    <label>Your Email: <input type="email" name="email" /></label>
  </p>
  <p>
    <label>Your Role: <select name="role[]" multiple>
      <option value="leader">Leader</option>
      <option value="follower">Follower</option>
    </select></label>
  </p>
  <p>
    <label>Message: <textarea name="message"></textarea></label>
  </p>
  <p>
    <button type="submit">Send</button>
  </p>
</form>
```

Notice that we've set the form method to POST instead of the default GET and we're using `data-netlify="true"`attribute rather than `netlify` attribute. This attribute is necessary for Netlify to be able to find your form.

I found that this POST was still leading to a 404 and, after scouring the [interwebs](https://community.netlify.com/t/form-and-gatsby-404-on-submit/381/13), I found that we also need to add `<input type="hidden" name="form-name" value="<name-of-form>" />` (In our case, <name-of-form> will be "contact") so that the full HTML is:
    
```html
<form name="contact" method="POST" data-netlify="true">
    <input type="hidden" name="form-name" value="contact" />
  <p>
    <label>Your Name: <input type="text" name="name" /></label>   
  </p>
  <p>
    <label>Your Email: <input type="email" name="email" /></label>
  </p>
  <p>
    <label>Your Role: <select name="role[]" multiple>
      <option value="leader">Leader</option>
      <option value="follower">Follower</option>
    </select></label>
  </p>
  <p>
    <label>Message: <textarea name="message"></textarea></label>
  </p>
  <p>
    <button type="submit">Send</button>
  </p>
</form>
```

Aside from the debugging, forms is a great feature that typically necessitates server side code and maybe a database. Netlify saw how useful form submissions are and decided to make that available for everyone!
