+++
date = '{{ .Date }}'
draft = true
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
# Keep the tag vocabulary small: firmware, hardware, career (carreira in pt-br).
# One tag per post, two at most. Add a new tag only when you expect several
# future posts to use it too.
tags = []
+++
