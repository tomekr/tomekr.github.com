---
layout: post
title: 'Rails Security #1: Sessions'
category: posts
---

rails/actionpack/lib/action_dispatch/middleware/session/cookie_store.rb

 > This cookie-based session store is the Rails default. Sessions typically
 > contain at most a user_id and flash message; both fit within the 4K cookie
 > size limit. Cookie-based sessions are dramatically faster than the
 > alternatives.

In regards to the digest at the end of the cookie...

 > A message digest is included with the cookie to ensure data integrity:
 > a user cannot alter his +user_id+ without knowing the secret key
 > included in the hash. New apps are generated with a pregenerated secret
 > in config/environment.rb. Set your own for old apps you're upgrading.

```ruby
session_data << "--#{generate_hmac(session_data, @secrets.first)}"
```

- Rails uses [Rack][rack] to generate rack sessions

[rack]: https://github.com/rack/rack/blob/master/lib/rack/session/abstract/id.rb

