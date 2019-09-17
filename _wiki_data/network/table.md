---
title: sample network
description: ネットワーク構成図
---


## 論理構成

{% nwdiag %}
nwdiag {
  gateway [shape = cloud];
  gateway -- FWX120;
  network home {
    address = "10.20.0.0/24"

    FWX120  [address = "10.20.0.254"];
    WLX202 [address = "10.20.0.253"];
    NETGEAR_JGS524PE [address = "10.20.0.252"];
    RaspberryPi [address = "10.20.0.1"];
    PS4 [address = "10.20.0.2"];
    NintendoSwitch [address = "10.20.0.3"];
  }
  network dmz {
    address = "10.21.0/24"

    FWX120  [address = "10.21.0.254"];
    StorageServer [address = "10.21.0.2"];
    ReverseProxyServer [address = "10.21.0.4"];
    BotServer [address = "10.21.0.5"];
  }
  network guest {
    address = "10.22.0.0/24"
    FWX120  [address = "10.22.0.254"];
    guest_smart_phone1 [address = "10.22.0.1"];
    guest_smart_phone2 [address = "10.22.0.2"];
    guest_smart_phone3 [address = "10.22.0.3"];
  }
}
{% endnwdiag %}

## 物理構成
{% blockdiag %}
  blockdiag {
    FWX120 [label = "FWX120"];
    SWX2100-5PoE [label = "SWX2100-5PoE"];
    WLX202 [label = "WLX202"];
    NETGEAR_JGS524PE [label = "NETGEAR_JGS524PE"];
    PS4 [label = "PS4"];
    NintendoSwitch [label = "NintendoSwitch"];
    
    // wifi
    SSID_DoiHomeWiFi [label = "DoiHomeWiFi"];
    SSID_DoiGuestWiFi [label = "DoiGuestWiFi"];

    FWX120 -> NETGEAR_JGS524PE [label = "vlan 1,2,3", fontsize = 6];
    NETGEAR_JGS524PE -> SWX2100-5PoE [label = "vlan 1,3", fontsize = 6];
    SWX2100-5PoE -> PS4 [label = "vlan 1", fontsize = 6];
    SWX2100-5PoE -> NintendoSwitch [label = "vlan 1", fontsize = 6];
    SWX2100-5PoE -> WLX202 [label = "vlan 1,3", fontsize = 6];

    WLX202 -> SSID_DoiHomeWiFi [label = "vlan 1", fontsize = 6];
    WLX202 -> SSID_DoiGuestWiFi [label = "vlan 3", fontsize = 6];

    NETGEAR_JGS524PE -> RaspberryPi [label = "vlan 1", fontsize = 6];
    NETGEAR_JGS524PE -> StorageServer [label = "vlan 2", fontsize = 6];
    NETGEAR_JGS524PE -> ReverseProxyServer [label = "vlan 2", fontsize = 6];
    NETGEAR_JGS524PE -> BotServer [label = "vlan 2", fontsize = 6];
    
    group rack{
      label = "ラックの中";
      color = "#77FF77";

      FWX120;NETGEAR_JGS524PE;StorageServer;ReverseProxyServer;BotServer;
    }

    group tv{
      label = "TV台";
      color = "#51a6ff";
      SWX2100-5PoE;WLX202;PS4;NintendoSwitch;
    }

    group {
      label = "WiFi";
      color = "#FF0000";
      shape = line;
      style = dashed;
      SSID_DoiHomeWiFi;SSID_DoiGuestWiFi;
    }


  }
{% endblockdiag %}

### ラック配置図
{% rackdiag %}
rackdiag {
  19U;

  19: FWX120;
  17: StorageServer [2U]
  15: NETGEAR_JGS524PE
  13: SG300-52
  12: IBM system X3550 m3
}
{% endrackdiag %}

