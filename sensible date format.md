---
tags:
  - date
  - format
  - logs
  - script
  - time
  - timestamp
  - epoch
  - notam
---

To get a date and time in a sensible, human readable, format:

    date +'%F %T'

For a sortable and readable timestamp without spaces (used in raw format
notams):

     date +%Y%m%d%H%M

Timestamp in seconds since epoch:

    date +%s

*Bonus tip:* What date is it next sunday?

    date +%F --date='next sunday'
