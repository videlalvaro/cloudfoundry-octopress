# cloudfoundry-octopress #

This project eases the deployment of [octopress](http://octopress.org/) blogs to [Cloud Foundry](http://cloudfoundry.com/).

## Requirements ##

- A Cloud Foundry account. Get one [here](https://my.cloudfoundry.com/signup).
- Octopress installed. Follow the setup steps from the octopress [website](http://octopress.org/docs/).
- `vmc` installed: `gem install vmc`
- Some ideas to blog about.

## Instructions ##

We assume that you cloned octopress in a folder called `octopress` and that you followed steps explained in their [setup instructions](http://octopress.org/docs/setup/).

```bash
cd /path/to/octopress
git clone git://github.com/videlalvaro/cloudfoundry-octopress.git
```

Now we are going to genereate the basic files for our Cloud Foundry applications. Let's call it `myblog`.

```bash
rake --rakefile cloudfoundry-octopress/Rakefile new_app["myblog]
```

At this point we have a basic app to serve our blog. Let's add our first blog post using rake:

```bash
rake new_post["Hello Octopress"]
```

Then write the blog post inside the `source/_posts/YYYY-MM-DD-hello-octopress.markdown` file.

Once you finished writing your blog post run the following rake task to generate the blog static files:

```bash
rake generate
```

And now we are ready to push our blog to Cloud Foundry

```bash
vmc push
Would you like to deploy from the current directory? [Yn]: Y
Pushing application 'myblog'...
Creating Application: OK
Uploading Application:
  Checking for available resources: OK
    Processing resources: OK
      Packing application: OK
        Uploading (36K): OK
        Push Status: OK
        Staging Application 'myblog': OK
        Starting Application 'myblog': OK
```

Now the next time you add a new blog post instead of running `vmc push` simply run `vmc update`

## License

Copyright © 2012 Alvaro Videla <avidela@vmware.com>

See the LICENSE file.
