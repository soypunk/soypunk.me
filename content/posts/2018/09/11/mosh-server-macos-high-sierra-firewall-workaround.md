---
title: ""
slug: "mosh-server-macOS-high-sierra-firewall-workaround"
date: "2018-09-11T11:38:19-07:00"
draft: false
tags:
- mosh
- macOS
- hacking
2018:
 - "09"
archives:
 - "2018/09/11"
---

Was having all sorts of problems [running mosh-server on macOS High Sierra until I found this workaround buried in a github issue][1]:

    # i recommend setting up the following alias first
    alias firepower='sudo /usr/libexec/ApplicationFirewall/socketfilterfw'
    
    # temporarily shut firewall off
    firepower --setglobalstate off
    
    # add symlinked location to firewall
    firepower --add $(which mosh-server)
    firepower --unblockapp $(which mosh-server)
    
    # add homebrew location to firewall
    firepower --add $(brew --prefix)/Cellar/mosh/1.3.2_2/bin/mosh-server
    firepower --unblockapp $(brew --prefix)/Cellar/mosh/1.3.2_2/bin/mosh-server
    
    # re-enable firewall
    firepower --setglobalstate on
  
Nothing else worked, so bless you [Jay Schwartz][2]. Note: you have to repeat this magic every time you update mosh-sever to a new version. Awesome.

[1]: https://github.com/mobile-shell/mosh/issues/898#issuecomment-368333946
[2]: https://github.com/JayTheMarketer