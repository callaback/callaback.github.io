---
category: AI / Image Generation
path: '/api/text-to-image'
title: 'GET Text-to-Image Generation'
type: 'GET'
layout: null
---


# Basic
curl -o output.png "https://text-to-image.callaback.com/?prompt=cat"

# With multiple parameters
curl -o cat_portrait.png \
  "https://text-to-image.callaback.com/?prompt=portrait%20of%20a%20cat&num_steps=30&width=512&height=512"

# URL-encoded complex prompt
curl -o fantasy_cat.png \
  "https://text-to-image.callaback.com/?prompt=a%20magical%20cat%20with%20wings%20in%20a%20fantasy%20forest"
  

- prompt=abstract%20colorful%20cat%20silhouette
- prompt=geometric%20cat%20made%20of%20cubes
- prompt=neon%20glowing%20cat%20in%20darkness
- prompt=cat%20in%20a%20spaceship%20cockpit
- prompt=steampunk%20cat%20with%20mechanical%20gears
- prompt=cat%20as%20a%20medieval%20knight
- prompt=cat%20in%20the%20style%20of%20van%20gogh
- prompt=anime%20style%20warrior%20cat
- prompt=watercolor%20painting%20of%20a%20cat
- prompt=fluffy%20white%20kitten%20sleeping
- prompt=lion%20in%20the%20savannah%20sunset
- prompt=panda%20eating%20bamboo%20in%20forest


# Parameter Tips:

num_steps: 20-30 for good quality, 10-15 for faster results
guidance_scale: 7.0-9.0 for balanced results
seed: Use the same seed with same prompt for identical results
width/height: Use multiples of 64 for best results
