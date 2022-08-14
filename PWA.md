# Serving
## Caching strategies
- Cache First

  - Search for a cached response first and falls back to the network if one isn't found.
  
    ```js
  self.addEventListener("fetch", event => {
  caches.match(event.request)
  .then(cachedResponse => {
  return cachedResponse || fetch(event.request)
      })
      })
    ```
- Network First

  - Same cache first; but check request fulfilled first
  
  ```js
  self.addEventListener("fetch", event=>{
      fetch(event.request)
      .cach(err => 
      caches.match(event.request)
      )

      })

  ```
- Stale while revalidate

  - The assets are updated in the background. User will get newest version after requested.
  
  ```js
  self.addEventListener("fetch", event =>{
      event.responWith(
          caches.math(event.request).then(cachedResponse =>{
            const networkFetch = fetch(event.request).then(response => {
              caches.open("assets").then(cache =>{
              cache.put(event.request, response.clone())
              })
            })
      return cachedResponse || networkFetch
            })
          )
      })
  ```
- Network Only
- Cache only
