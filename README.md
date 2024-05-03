# URL Tracker Tests

A quick UI for testing URL trackers. Some browsers are starting to filter them so check them here. 

I think it is a good idea to remove the generated user-specific trackers like `fbclid` but general attribution trackers like `utm_source` are incredibly useful for businesses. They should be respected and retained.

Firefox does do some different filtering with `privacy.query_stripping.enabled` based on if the link came from the current site or not. I'll probably do something for that in the future.