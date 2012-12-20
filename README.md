# cloudfoundry-octopress #

This project eases the deployment of [Octopress](http://octopress.org/) blogs to [Cloud Foundry](http://cloudfoundry.com/).

See a sample blog here: [http://octofoundry.cloudfoundry.com](http://octofoundry.cloudfoundry.com).

## Requirements ##

- A Cloud Foundry account. Get one [here](https://my.cloudfoundry.com/signup).
- Octopress installed. Follow the setup steps from the Octopress [website](http://octopress.org/docs/).
- `vmc` installed: `gem install vmc`
- Some ideas to blog about.

## Instructions ##

We assume that you cloned the Octopress git repository in a folder called `octopress` and that you followed steps explained in their [setup instructions](http://octopress.org/docs/setup/). 

So - before continuing - you should already have a folder called `octopress` and you should also have edited the `_config.yml` file to provide some useful configuration for your blog such as a sensible title, authorship information, etc.. You may also wish to choose and install one of the many available [Octopress themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes).

```bash
cd /path/to/octopress
git clone git://github.com/videlalvaro/cloudfoundry-octopress.git
```

Now we are going to generate the basic files for our Cloud Foundry application. Let's call this one `myblog`.

```bash
rake --rakefile cloudfoundry-octopress/Rakefile new_app["myblog"]
```

> if you see an error whilst running this command, it is possible you are using zsh as your chosen shell. There is a problem with the way in which zsh uses globbing when using rake commands. See [Octopress issue #117](https://github.com/imathis/octopress/issues/117) for several workarounds, or simply use a different shell such as bash.

At this point we have a basic app to serve our blog. Let's add our first blog post using rake:

```bash
rake new_post["Hello Octopress"]
```

Then write the blog post inside the `source/_posts/YYYY-MM-DD-hello-octopress.markdown` file.

Once you finished writing your blog post, run the following rake task to generate the static blog files:

```bash
rake generate
```

Before deploying, you should also double-check the `_config.yml` file to ensure that the url value matches the expected final URL that you are deploying to.

Now we are ready to push our blog to Cloud Foundry

```bash
vmc push
Using manifest file manifest.yml
Creating myblog... OK
Updating myblog... OK
Uploading myblog... OK
Starting myblog... OK
Checking myblog... OK
```

Now the next time you add a new blog post, simply repeat the `vmc push` command.

## License

Copyright © 2012 Alvaro Videla <avidela@vmware.com>

See the LICENSE file.
