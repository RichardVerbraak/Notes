# Random Notes

Notes that still have to be sorted and put in it's respective file

## CSR vs SSR

Details and pros & cons of the types of rendering

### Client Side Rendering (CSR)

Client side rendering is used by Create-React-App by serving up an empty HTML file -
with only a bundled file of JS and CSS assets (bundled by Webpack).
The browser then run the .js file which in turn generates the actual content and then render it.

#### Pros

    -   Navigating between pages is fast
        -   All HTML is generated on the client side which makes the page feel app-like and thus fast
    -   All resources are in one file and so you don't have to request anything else
    -   Fetched data will update the page in real time (reactive)

#### Cons

    -   Initial page load is slow
        -   All JS and CSS files are compiled in a single bundle, this takes a lot of time to process
    -   No SEO
        -   The server sends a blank HTML file initially so without a single word of content to web crawl through
    -   Page won't even render if JavaScript is disabled since the bundle.js file contains everything the page needs

### Server Side Rendering (SSR)

Server side rendering is

#### Pros

    -   Has SEO since the entire page is already built
    -   Fully interactive when the page is visible
    -   Will still display the page even if JS is disabled (pre-built on the server)

#### Cons

    -   Navigating between pages is slower
        -   Requests to the server have to be made each time causing full-page reloads
    -   Increase server load due to all of these requests
    -   Since the HTML is built on the server it is not "reactive" on the front-end and cannot fetch/update data in real time like CSR

### Static Site Generators (SSG)
