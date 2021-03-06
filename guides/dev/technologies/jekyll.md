# shell
## setup
    sudo apt install ruby-full build-essential zlib1g-dev 
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    gem install jekyll bundler
## use
    //new    
        //with scaffolding, --blank: blank jekyll scaffold
            jekyll new [path] {}? 
        //theme scaffold
            jekyll new-theme
    //if not using scaffolding, manually add Gemfile
            bundle init
            vim  Gemfile 
                gem "jekyll"
            bundle install
            //use "bundle exec jekyll" to use local version of jekyll
    //build
        //output build to _site
        jekyll build
        //above, rebuild after any changes and run server
        jekyll serve
# project layout
    Gemfile //Gemfile lists required packages (gems)
    Gemfile.lock
    _config.yml //config
    _data //site data: .yml ,yaml json .csv .tsv
        members.yml
    _drafts //unpublised posts
        begin-with-the-crazy-ideas.md
        on-simplicity-in-technology.md
    _includes //partials to use between layouts
        footer.html
        header.html
        navigation.html
    _layouts //templates that wrap posts
        default.html
        post.html
    _posts //dynamic content
        2007-10-29-why-every-programmer-should-play-nethack.md
        2009-04-26-barcamp-boston-4-roundup.md
    _sass
    _base.scss
    _layout.scss
    _site //generated site
    .jekyll-metadata //keep track of what files have/havent changed
    index.html # can also be an 'index.md' with valid front matter
    //additional
        assets
            class   
            images
            js
        _collectionNane //custom collection declared in config.yml   

# liquid 
    //access (from corresponding folder)
        //data
            site.data.fileName
        //includes
            {% include navigation.html %}
        //posts
            site.posts.fileName
        //collections
            site.collectionName
        //environment variables
            jekyll.environment
# front matter
    //access (from corresponding folder)
        //layout
            layout: fileName
    //front matter defaults
//collections
    //custom jekyll folders
//env variables
    //preset var in shell for jekyll to use, eg to distinguish production modes

# tutorial
## liquid templating language
        obj: where to output content
            {{ page.title }}
        tags: create logic and control flow for templates
            {% if page.show_sidebar %}
              <div class="sidebar">sidebar content</div>
            {% endif %}
        filters: change output og liquid obj
            {{ "hi" | capitalize }}
        //front matter
            YAML snippet inbetween ---  ---
            set variables for the page
                ---
                title: Home
                ---
                <title>{{ page.title }}</title>
## layouts
    //EG _layouts/default.html
        <!doctype html>
        <html>
          <head>
            <meta charset="utf-8">
            <title>{{ page.title }}</title>
          </head>
          <body>
            {{ content }}
          </body>
        </html>
    //EG post.html, using _layouts/default.html
        ---
        layout: default
        ---
        <h1>{{ page.title }}</h1>
        <p>{{ page.date | date_to_string }} - {{ page.author }}</p>
        {{ content }}

## includes
    //EG navigation, use page.url to help set styling
       <nav>
        <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>Home</a>
        <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>About</a>
       </nav>  
## data
    //EG make navigation more efficient
        //_data/navigation.yml
        - name: Home
        link: /
        - name: About
        link: /about.html
        //then includes/navigation.html
        <nav>
          {% for item in site.data.navigation %}
            <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
              {{ item.name }}
            </a>
          {% endfor %}
        </nav>     
## assets
    //copied across to build site
## sass
    /assets/css/styles.scss
        ---
        ---
        @import "main";
    //will import _sass/main.scss
    //can use with
    <link rel="stylesheet" href="/assets/css/styles.css">
## posts
## collections
    //EG _config.yml
        collections:
          authors:
    then can add files in _authors
## front matter defaults
    config.yml
        collections:
          authors:
            output: true
        defaults:
          - scope:
              path: ""
              type: "authors"
            values:
              layout: "author"
          - scope:
              path: ""
              type: "posts"
            values:
              layout: "post"
          - scope:
              path: ""
            values:
              layout: "default" 
## plugins
### file setup
    mkdir _plugins
    vim _config.yml
       plugins:
         - jekyll-feed
         - jekyll-sitemap
         - jekyll-seo-tag
    gem install jekyll-sitemap jekyll-feed jekyll-seo-tag 
    vim Gemfile
        source 'https://rubygems.org'
        gem 'jekyll'
        group :jekyll_plugins do
          gem 'jekyll-sitemap'
          gem 'jekyll-feed'
          gem 'jekyll-seo-tag'
        end

## environment
    JEKYLL_ENV=production bundle exec jekyll build
    {% if jekyll.environment == "production" %}
      <script src="my-analytics-script.js"></script>
    {% endif %}
