# Micro.blog Category Map

A lightweight, responsive map integration for Micro.blog (and other Hugo-based sites) that automatically generates interactive markers based on a data file. It uses **Leaflet.js** and **OpenStreetMap**, so no API keys are required.

## Disclaimer

The ideas and implementation logic for this project were conceived by me, but as I am not a developer, the code itself was generated with the assistance of AI. While the tool works as intended for [my use case](https://vladcampos.com/map), I cannot attest to the quality of the code, its optimization, or its security. **Use this code at your own risk.**

## Repository Structure

To use this in your Micro.blog design settings, ensure your files are organized as follows:

- `data/cities.yml`: The list of locations, coordinates, and links.
    
- `layouts/partials/microblog-map.html`: The logic and script that renders the map.
    

## Installation

### 1. Add the Data

Create a file in your Micro.blog design area at `data/cities.yml` and add your locations following this format:

```
- name: "Boston, USA"
  slug: "boston"
  lat: 42.3601
  lon: -71.0589
  url: "/categories/boston"

- name: "Porto, Portugal"
  slug: "porto"
  lat: 41.1579
  lon: -8.6291
  url: "/categories/porto"

```

### 2. Add the Map Partial

Create a new template at `layouts/partials/microblog-map.html` and paste the code provided in this repository.

### 3. Load the Assets (Head)

You need to load the Leaflet CSS and JavaScript.

- **Tiny Theme users:** Add this to `layouts/partials/microhook-head.html`.
    
- **Other themes:** Add this to your `head.html` partial or header template.
    

```
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

```

### 4. Include the Script (Footer)

Add the following line to your footer to load the map logic:

- **Tiny Theme users:** Add this to `layouts/partials/microhook-footer.html`.
    
- **Other themes:** Add this to your `footer.html` partial.
    

```
{{/* Safety check: Only call the partial if Hugo can find the file.
  This prevents "partial not found" errors from breaking the site build.
*/}}
{{ if templates.Exists "partials/microblog-map.html" }}
    {{ partial "microblog-map.html" . }}
{{ end }}

```

### 5. Display the Map

Place the following HTML on any page, post, or template where you want the map to appear:

```
<div id="categoryMap" style="width: 100%; height: 400px; border-radius: 12px;"></div>

```

## How it Works

The script specifically looks for an element with the ID `categoryMap`. If it doesn't find that element on a page, the script exits silently, ensuring your site remains fast. When it finds the ID, it pulls data from `cities.yml` and automatically centers the map to fit your markers.

## License

MIT - Feel free to use and modify for your own blog!
