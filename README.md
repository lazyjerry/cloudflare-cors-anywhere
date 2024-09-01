# cloudflare-cors-anywhere
Cloudflare CORS proxy in a worker.

CLOUDFLARE-CORS-ANYWHERE

Jerry 添加一個 PROXY_AUTH 作為 key 防止濫用
如果 PROXY_AUTH 有值，則必須在 header 中 proxy-auth 帶上相對應參數

Blog Post:
https://hipster.crazyjerry.studio/post/%e4%bd%bf%e7%94%a8-cloudflare-workers-%e8%99%95%e7%90%86%e5%89%8d%e7%ab%af%e8%b7%a8%e5%9f%9f%e5%95%8f%e9%a1%8c/

Source:
https://github.com/Zibri/cloudflare-cors-anywhere

Demo:
https://test.cors.workers.dev

Donate:
https://paypal.me/Zibri/5

Post:
http://www.zibri.org/2019/07/your-own-cors-anywhere-proxy-on.html

## Deployment

This project is written in [Cloudfalre Workers](https://workers.cloudflare.com/), and can be easily deployed with [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/).

```bash
wrangler publish
```

## Usage Example

```javascript
fetch('https://test.cors.workers.dev/?https://httpbin.org/post', {
  method: 'post',
  headers: {
    'x-foo': 'bar',
    'x-bar': 'foo',
    'x-cors-headers': JSON.stringify({
      // allows to send forbidden headers
      // https://developer.mozilla.org/en-US/docs/Glossary/Forbidden_header_name
      'cookies': 'x=123'
    }) 
  }
}).then(res => {
  // allows to read all headers (even forbidden headers like set-cookies)
  const headers = JSON.parse(res.headers.get('cors-received-headers'))
  console.log(headers)
  return res.json()
}).then(console.log)
```

Note:

All received headers are also returned in "cors-received-headers" header.

Note about the DEMO url:

Abuse (other than testing) of the demo will result in a ban.  
The demo accepts only fetch and xmlhttprequest.  

To create your own is very easy, you just need to set up a cloudflare account and upload the worker code.  

My personal thanks to Damien Collis for his generous and unique donation.    

