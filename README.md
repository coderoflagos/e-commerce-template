
## Documentation for Bartholomew's E-commerce Templates (For Frontend)

### Utilizing the Template

This is just a quickstart example of the Bartholomew CMS E-commerce Template. In this quickstart section, we use the latest Bartholomew E-commerce template, which contains a lot of prebuilt parts (for your convenience). The template works with Handlebars and different Markdown files for its content.

### Getting Started

Next, we can now generate a new repository with the same directory and file structure. Simply visit [the template's location on GitHub](https://github.com/coderoflagos/e-commerce-template), then click the “Use this template” button and follow the prompts. 

![GitHub repo](https://i.postimg.cc/QxBSJckr/image2.png)

### Fetch Your Site

Clone your repository, which you created in the previous step:

```
$ git clone <your-github-account> <your-repo-name>
```
### Navigate to your newly cloned repository:

```
$ cd <your-repo-name>
```

### Bartholomew CLI 

For the Bart CLI, install all the assets in Bartholomew's official releases just as you have [here](https://github.com/fermyon/bartholomew/releases/tag/v0.6.0).

### ```spin up``` Your Site

Run the ```spin up``` command to launch your site on ```localhost```:

```$ spin up --follow-all```

When you navigate to ```localhost:3000```, you should see your website running.

### Creating your Content

In this case, you will have to create your pages manually. You will notice we have almost everything ready, you could choose to add more files or delete some. All your contents run directly from the ```content/``` section. Creating your contents starts with creating the files in different directories under the ```content/``` folder. In this case, you’ll see we have ```content/latest```, ```content/kids```, ```content/cart```, etc. You have to create some Markdown files under it to see your contents, and signify the template the Markdown file should work with. 

Here’s the structure of a random file in the ```latest/``` directory:

```
title = "First Item"
template = "blog"
 
[extra]
type = "post"
product_description = "Whatever is in here"
section = "men"
price = "$70"
tag = "hoodies"
photo-src = "https://i.postimg.cc/h4z0vNrZ/Real-Madrid-Hoodie-Jacket-Pants-Training-Suit-Light-Grey-2019-20-removebg-preview.png"
---

```

The first three lines of the code above are essential information for markdown files that work with Bartholomew. Firstly, you need to know that every markdown file is a page in Bartholomew. The ```title = “FirstItem"``` code says the title of the page should be **First Item**. The ```template = “blog”``` meta specifies the template the file should use for its UI. In this case, the file will use the ```blog.hbs``` template. 

The other meta items under the ```[extra]``` section are not the basic ones, they are called the "extra information." The metas’ work with the strings that call them out in the specific template they work with. 

### Viewing your Site!

With this template, what you could do is modify the contents or add more files and create contents in them. Here’s how you should view your site:

![Template's UI](https://i.postimg.cc/yY1GHJHJ/image1.jpg)

Firstly, site configuration is super important, and you can find that in ```config/site.toml```. The most important part of this is the ```index_site_pages``` section. This is actually for the templates that should be indexed. Here’s what we have in the ```config/site.toml``` file for the e-commerce template: 

```index_site_pages = ["main", "blog", "allmen", "allwomen", "kids", "cart", "checkout"]```

The only two missing files are ```content_top.hbs``` and ```content_bottom.hbs```, which work with ```main.hbs```. The ```main.hbs``` file is the middle and the main part of the whole template, so it has to be indexed. For the ```blog.hbs``` file, it does not rely on ```content_top.hbs``` to give it a header, and the same applies to all other pages, except the ```main.hbs```. The ```content_top.hbs``` and ```content_bottom.hbs``` are just for the header and footer. 

For the templates, we have different files under the ```templates/``` directory. We have some files in the directory already — starting with ```content_top.hbs``` ```main.hbs``` to ```content_buttom.hbs```, etc. 
The ```content_top.hbs``` is for the UI of the header section of the index page, the header includes the navbar and its hero section after. The content for the ```content_top.hbs``` templates works with the ```index.md``` file. The ```main.hbs``` file is connected with the ```content_top.hbs``` file. The ```main.hbs``` file contains the main section of the file (where the “Latest”, “View All”, and “Join our waitlist” sections are). At the end of the ```main.hbs``` file, you will see the ```{{>content_bottom}}``` code. For the latest section – there’s a code in the ```main.hbs``` section that calls out the pages in the ```latest/``` directory, and here it is:

```
{{#each (blogs site.pages "/content/latest/")}}
```

For the ```kids.hbs``` works with the ```kids/``` directory. All that connects each markdown in every directory with its UI is the ```template = templatename``` code. In this case, for kids, we used the ```template = blog```, and that’s why the files under the ```content/kids/``` directory work with the ```blog.hbs``` template. The same applies to other files in the directories under the ```content/``` directory.

### How to add a new item

In this template, adding an item is equivalent to creating a page. Here’s how you can add a file for each directory:

To create a latest item — it should be in the file you’re creating has to be in the ```content/latest/``` folder just like this:

```./bart new post content/latest filename.md --template = blog```

For creating an item for men, the file you’re creating should be in the ```content/menlisting``` folder just like this:

```./bart new post content/menlisting filename.md --template = blog ```

To create an item for kids, the file you are creating has to be in the ‘content/kids’ folder just like this:

```./bart new post content/kids filename.md --template = blog```

To create an item for women, the file you are creating has to be in the ```content/womenlisting``` folder just like this:

```./bart new post content/womenlisting filename.md --template = blog```

Creating items for the store is just as easy as that, all you have to do is run any of the commands above in your terminal.

### How to add an image of a product

To do this, you need to navigate to the Markdown you created under the ‘[extra]’ section. Here’s a way to do it, it should be after the ‘[extra]’ section of the Markdown:

```photo-src = “photofolder/photoname.png```

How to change the price of an Item

It's easy to do this, as all you need to do is this right after the ```[extra]``` section too:

```price = “$price” ```

To learn more about how Bartholomew's templates work, you can check out this document. You also need to [learn about how the site configuration works](https://bartholomew.fermyon.dev/configuration) if you want to learn how to work with the templates.

