## PUBLIC README

2022 masama matsing
CLoudflare pages
no *.domain.com
HUGO_VERSION 0.88.1


width="100%" height="auto"

7 dimensions, 5 layers, 4 thermodynamics, 3 states, 2 forces, 1 observer (yourself)


https://cdn.jsdelivr.net/gh/alpinejs/alpine@v3.5.0/dist/alpine.min.js

js toggle div


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
