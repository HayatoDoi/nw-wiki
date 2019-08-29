---
title: table network
description: 机の上のネットワーク構成図
---


## 構成

{% nwdiag %}
nwdiag {
  network wan {
      address = "10.0.0.1/30"
 
      RTX830  [address = "10.0.0.1"];
      RTX1210 [address = "10.0.0.2"];
  }
}
{% endnwdiag %}

### RTX830

### RTX1210

