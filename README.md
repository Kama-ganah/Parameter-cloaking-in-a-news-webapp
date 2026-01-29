# Overview
During an assessment of the application’s caching behavior, I identified a high-severity web cache poisoning vulnerability caused by parameter cloaking. The application’s caching layer failed to include certain query parameters in the cache key, while the back-end server still parsed and executed them. By cloaking a malicious parameter inside an unkeyed analytics parameter, I was able to poison a shared cache entry and deliver arbitrary JavaScript to all users loading the affected resource.

# Steps Undertaken

Step 1: Analyzed cache behavior on static JavaScript resources and identified parameters excluded from the cache key.

Step 2: Used Burp Suite and Param Miner to enumerate unkeyed and cloaked parameters.

Step 3: Identified a JSONP endpoint that executed a user-controlled callback parameter.

Step 4: Injected a second callback parameter cloaked inside an unkeyed parameter using a semicolon delimiter.

Step 5: Sent a crafted request to poison the cache with a malicious JavaScript payload.

Step 6: Verified that subsequent users received the poisoned cached response, triggering JavaScript execution in their browsers.

# Conclusion

This assessment confirmed a critical web cache poisoning vulnerability via parameter cloaking. Inconsistent parameter parsing between the cache and back-end allowed attackers to inject and persist malicious JavaScript across user sessions without authentication or direct interaction. Proper cache key management, consistent request parsing, and elimination of unsafe patterns such as JSONP are essential to prevent large-scale client-side compromise.
