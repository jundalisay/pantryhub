## PUBLIC README

CLoudflare pages
no *.domain.com
HUGO_VERSION 0.88.1

7 dimensions, 5 layers, 4 thermodynamics, 3 states, 2 forces, 1 observer (yourself)

                <a href="{{.Permalink}}" title="{{ i18n "readmore" }} - {{ .Title }}" class="button is-primary" style="position: absolute; bottom: 15px !important; margin: none !important;">{{ i18n "readmore" }}</a>

<!-- checking blog -->
<!-- {{ if or (or (eq .Section "post") (eq .Section "blog")) (or (eq .Section "categories") (eq .Section "tags") )}} -->


enable  : true
galleryImages :
  - image : images/portfolio/item-1.jpg
  - image : images/portfolio/item-2.jpg
  - image : images/portfolio/item-3.jpg
  - image : images/portfolio/item-4.jpg
  - image : images/portfolio/item-5.jpg
  - image : images/portfolio/item-6.jpg

clients.yml
enable        : true
title         : "Who trust our judgment"
client_logos  : 
  ["images/clients/client-logo-one.png", "images/clients/client-logo-two.png", "images/clients/client-logo-three.png", "images/clients/client-logo-four.png", "images/clients/client-logo-five.png", "images/clients/client-logo-six.png", "images/clients/client-logo-seven.png", "images/clients/client-logo-eight.png", "images/clients/client-logo-nine.png", "images/clients/client-logo-ten.png"]


{{ with .Site.Data.clients }}
  {{ if .enable }}
  <section class="site-client">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="section-title">
            <h2>{{ .title }}</h2>
          </div>
          <div class="site-client-wrapper">
            {{ range .client_logos }}
            <div class="site-client-item">
              <img src="{{ . | absURL }}" alt="client-logo">
            </div>
            {{ end }}
          </div>
        </div>
      </div>
    </div>
  </section>
  {{ end }}
{{ end }}


https://cdn.jsdelivr.net/gh/alpinejs/alpine@v3.5.0/dist/alpine.min.js

{{ $styles := slice }}

{{ range site.Params.plugins.css }}
  {{ if findRE "^http" .link }}
    <link crossorigin="anonymous" media="all" rel="stylesheet" href="{{ .link | absURL }}" {{.attributes | safeHTMLAttr}} >
  {{ else }}
    {{ $styles = $styles | append (resources.Get .link) }}
  {{ end }}
{{ end }}

{{ $styles := $styles | append (resources.Get "scss/style.scss" | resources.ExecuteAsTemplate "style.scss" . | toCSS) }}

{{ $styles := $styles | resources.Concat "/css/style.css" | minify  | fingerprint "sha512"}}

<style crossorigin="anonymous" media="all" type="text/css" integrity="{{ $styles.Data.Integrity }}">{{$styles.Content | safeCSS}}</style>



  {{ if hugo.IsProduction }}
  {{ partialCached "style.html" . }}
  {{ else }}
  {{ partial "style.html" . }}
  {{ end }} 


  <section class="section my-5">
    <div class="container has-text-centered my-5">
      <h2 class="title is-2">{{ .title | markdownify }}</h2>

      <div class="" x-data="{ tab: window.location.hash ? window.location.hash.substring(1) : '1' }" id="tab_wrapper">
        <div class="tabs is-toggle is-toggle-rounded is-fullwidth are-small">
          <ul>
            <li><span class="h"><a :class="{ 'is-active': tab === '1' }" @click.prevent="tab = '1'; window.location.hash = '1'" href="#" >Step 1</a></span></li>
            <li><span class="h"><a :class="{ '': tab === '2' }" @click.prevent="tab = '2'; window.location.hash = '2'" href="#" >Step 2</a></span></li>
            <li><span class="h"><a :class="{ '': tab === '3' }" @click.prevent="tab = '3'; window.location.hash = '3'" href="#" >Step 3</a></span></li>            
          </ul>
        </div>
        {{ range .steps }}        
          <div class="columns is-mobile is-multiline" x-show="tab === '{{ .id }}'">
            <div class="column is-3-mobile is-2">
              <div class="card has-text-centered">
                <a href="{{ .link }}">
                  <img src="{{ .image | absURL }}" style="height: 100px; width: 100px;" class="card-image">
                </a>
                <p class="card-footer">{{ .content | markdownify }}</p>
              </div>
            </div>       
          </div>  
        {{ end }}
        </div>  
      </div>
    </div>
  </section>
{{ end }}
