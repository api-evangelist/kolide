---
title: "Improvements to Kolide Device Removal"
url: "https://www.kolide.com/blog/improvements-to-kolide-device-removal"
date: "2024-05-24"
feed_url: "https://www.kolide.com/blog.rss"
---
Previously, when you removed a device from Kolide, if the agent was still installed on the device, it would immediately re-enroll. Not great. To solve this in our legacy product, we introduced the concept of a Device Tombstone to prevent this re-enrollment.
