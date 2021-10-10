# Dynaaminen Versio

_**Me Armada Allianssissa rakennamme aktiivisesti tarvittavia ohjelmistopaketteja, joita tarvitaan Cardano stake poolin ylläpitoon ARM-pohjaisilla tietokoneilla, kuten Raspberry Pi:llä tai Applen MacMini M1:llä.**_

{% hint style="warning" %}
### Käyttääksesi dynaamista arm64 cardano-node versiota sinulla täytyy olla [libsodium](https://github.com/input-output-hk/libsodium) asennettuna.
{% endhint %}

{% hint style="success" %}
### Nykyinen Virallinen Cardano Node Versio: 1.30.1
{% endhint %}

### Yleiskatsaus 🗒

* [ ] Tarkista, onko libsodium asennettu paikalliseen koneeseen
  * Rakenna libsodium, jos ei ole jo asennettu
* [ ] Lataa Cardano Noden Dynaaminen versio & konfiguraatiotiedosto
* [ ] Pura tiedoston sisältö
* [ ] Tarkista, jos sinulla on jo Cardano Node -palvelu käynnissä
  * Sammuta Cardano node turvallisesti, jos se on käynnissä
* [ ] Korvaa vanhat binaarit uudella cardano-nodella ja cardano-cli:llä
* [ ] Tarkista, että cardano-node ja -cli versio on päivitetty nykyiseen versioon
* [ ] Korvaa vanhat asetustiedostot uusilla \(jos tarpeen\)
* [ ] Käynnistä Cardano node uudelleen
* [ ] Tarkista, että palvelin on käynnistynyt oikein

## Libsodiumin Rakentaminen

Tarkista ensin, onko libsodium jo asennettu.

```bash
which libsodium
```

Jos tämä ei palauta mitään tulostetta, sinun täytyy asentaa libsodium.

### Ohjeet libsodiumin asentamiseen

Luo työhakemisto omille rakennuksillesi:

```bash
mkdir -p ~/src
cd ~/src
```

Lataa ja asenna libsodium:

```bash
git clone https://github.com/input-output-hk/libsodium
```

```bash
cd libsodium
git checkout 66f017f1
```

```bash
./autogen.sh
```

```bash
./configure
```

```bash
make
sudo make install
```

Lisää seuraava .bashrc tiedostoon ja aseta lähde:

```bash
echo "export LD_LIBRARY_PATH="/usr/local/lib:$LD_LIBRARY_PATH"" >> ~/.bashrc

echo "export PKG_CONFIG_PATH="/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH"" >> ~/.bashrc

source ~/.bashrc
```

Ne, jotka suorittavat cardano-nodea järjestelmäpalveluna, käyttävät seuraavia toimintoja:

```text
sudo ldconfig
```

Tämä varmistaa, että järjestelmä on tietoinen libsodiumista \(ei vain käyttäjätasolla\).

## Lataa cardano-node & -cli

Dynamic binaries and Cardano node configuration files provided by [SRN pool ](https://armada-alliance.com/stake-pools/cc1b1c03798884c636703443a23b8d9e827d6c0417921600394198a0)🙏  at our [Github repository](https://github.com/armada-alliance/cardano-node-binaries).

```bash
wget https://github.com/armada-alliance/cardano-node-binaries/blob/main/dynamic-binaries/1.30.1/cardano-1_30_1-aarch64-ubuntu_2004.zip?raw=true
```

Extract the content from the zip file.

```bash
unzip cardano-1_30_1-aarch64-ubuntu_2004.zip?raw=true
```

### Check if cardano-node is running already

{% hint style="Huomaa" %}
**Now we need to make sure we do not have a cardano-node already running. If we do we must shut it down before proceeding.**
{% endhint %}

You can check if you have a cardano-node process already running a few ways like using`htop` or by checking your systemd service.

If you have been following our [Pi-Node guide](../pi-pool-tutorial/) you can check your cardano-node status and stop it using the following commands.

```bash
cardano-service status
cardano-service stop
```

{% hint style="info" %}
If you use Linux's `htop` service just check for a processing running starting with `cardano-node run` and use `SIGINT` to terminate the process.
{% endhint %}

## Replace the old binaries and config files with the new ones

If you are using the [Pi-Node guide](../pi-pool-tutorial/) and your cardano-node & cli in `~/.local/bin`

```bash
mv cardano-1_30_1-aarch64-ubuntu_2004/cardano-node cardano-1_30_1-aarch64-ubuntu_2004/cardano-cli ~/.local/bin
```

### Check your cardano-node version

```bash
cardano-node --version
```

#### Output:

```bash
cardano-node 1.30.1 - linux-aarch64 - ghc-8.10
git rev 0fb43f4e3da8b225f4f86557aed90a183981a64f
```

### Check your cardano-cli version

```bash
cardano-cli --version
```

#### Output:

```bash
cardano-cli 1.30.1 - linux-aarch64 - ghc-8.10
git rev 0fb43f4e3da8b225f4f86557aed90a183981a64f
```

### Replace the Cardano node configuration files

We have already downloaded the configuration files needed for three networks mainnet, testnet, and the alonzo-purple testnet.

{% tabs %}
{% tab title="Mainnet Config" %}
```bash
mv cardano-1_30_1-aarch64-ubuntu_2004/files/mainnet/* ~/pi-pool/files
```
{% endtab %}

{% tab title="Testnet Config" %}
```bash
mv cardano-1_30_1-aarch64-ubuntu_2004/files/testnet/* ~/pi-pool/files
```
{% endtab %}

{% tab title="Alonzo Purple Config" %}
```bash
mv cardano-1_30_1-aarch64-ubuntu_2004/files/alonzo-purple/* ~/pi-pool/files
```
{% endtab %}
{% endtabs %}

## Restart the Cardano Node

Now we just need to restart our cardano-node service if you are using our [Pi-Node guide](../pi-pool-tutorial/) use this command

```bash
cardano-service start
```

Wait a few seconds or so then check the status

```bash
cardano-service status
```



