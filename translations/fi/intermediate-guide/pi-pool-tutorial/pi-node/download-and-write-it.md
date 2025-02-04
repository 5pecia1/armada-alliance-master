---
description: Flash image
---

# Lataa & Polta

## Flash Image

Lataa, asenna & avaa [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager/releases/latest). Kytke USB-asema laittteeseen.

{% tabs %}
{% välilehden otsikko="Paikallinen kone \(Ubuntu\)" %}
```bash
# Ubuntu users can download and install with snapd
sudo apt update
sudo apt install snapd
sudo snap install rpi-imager
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
Vanhempien Pi4B 8GB mallien bootloader täytyy päivittää, jotta laite käynnistys USB portin kautta. Jos laitteesi ei käynnisty USB3 portista, käytä rpi-imager ohjelmaa ja tee Pi 4 EEPROM boot recovery sd kortti.

Kytke Pi monitoriin, aseta SD-kortti paikoilleen ja laita virta päälle. Kun näet vihreän näytön, laitteesi pitäisi olla valmis käynnistymään USB3 asemasta. Uudemmat RPi4B versiot toimitetaan bootloaderilla joka tukee valmiiksi USB-käynnistystä. **Feeling lucky?**

**Choose OS -&gt; Misc utility images -&gt; Raspberry Pi 4 EEPROM boot recovery** [https://www.raspberrypi.org/documentation/hardware/raspberrypi/booteeprom.md](https://www.raspberrypi.org/documentation/hardware/raspberrypi/booteeprom.md)
{% endhint %}

![](../../../.gitbook/assets/otgpoltut%20%281%29%20%281%29%20%281%29.png)

{% tabs %}
{% tab title="Pre configured Pi-Node.img.gz" %}
### Hanki Pi-Pool .img.gz tiedosto

| [Pi-Node](https://db.adamantium.online/Pi-Node.img.gz) |
|:------------------------------------------------------ |
|                                                        |


### Raspberry Pi Imager -ohjelmassa

**Choose OS -&gt; Use custom**

Locate the .img.gz file you downloaded & wish to flash.

Locate your target drive & write it to disk.

![](../../../.gitbook/assets/image-2-.png)
{% endtab %}

{% tab title="Fresh Ubuntu 21.04 installation" %}
### Raspberry Pi Imager -ohjelmassa

### Valitse Ubuntu Palvelin 21.04 \(RPI 3/4/400\)

**Choose OS -&gt; Other general purpose OS -&gt; Ubuntu -&gt; Ubuntu Server 21.04 \(RPI 3/4/400\)**. 64-bittinen palvelin vaihtoehto.

Etsi kohdeasema & kirjoita se levylle.

![](../../../.gitbook/assets/21.04-rpi-imager.png)
{% endtab %}
{% endtabs %}

