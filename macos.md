# Automatic .test local domains on macOS

> :book: Original source: [Automatic local domains: Setting up dnsmasq for macOS High Sierra using Homebrew](https://medium.com/@kharysharpe/automatic-local-domains-setting-up-dnsmasq-for-macos-high-sierra-using-homebrew-caf767157e43).

1. Install [Homebrew](https://brew.sh/).

2. Install [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html).

    ```bash
    brew install dnsmasq
    ```

3. Create config folder if it doesn’t already exist:

    ```bash
    mkdir -pv $(brew --prefix)/etc/
    ```

4. Configure dnsmasq for `*.test`:

    ```bash
    echo 'address=/.test/127.0.0.1' >> $(brew --prefix)/etc/dnsmasq.conf
    ```

5. Configure the listening port:

    ```bash
    echo 'port=53' >> $(brew --prefix)/etc/dnsmasq.conf
    ```

6. Start dnsmasq as a service so it automatically starts at login:

    ```bash
    sudo brew services start dnsmasq
    ```

7. Create a [DNS resolver](https://icannwiki.org/Domain_Name_Resolvers):

    ```bash
    sudo mkdir -v /etc/resolver
    sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/test'
    ```

8. Verify that all `.test` requests are using `127.0.0.1`:

    ```bash
    scutil --dns
    ```

   You should see something like this:

    ```text
    resolver #8
    domain   : test
    nameserver[0] : 127.0.0.1
    flags    : Request A records, Request AAAA records
    reach    : 0x00030002 (Reachable,Local Address,Directly Reachable Address)
    ```

   You can also test by using ping:

    ```bash
    ping dockerbox.test
    ```
