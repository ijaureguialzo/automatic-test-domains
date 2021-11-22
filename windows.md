# Automatic .test local domains on Windows

> :book: Original source: [Setup a dnsmasq equivalent on Windows (with Acrylic)](http://www.orbitale.io/2017/12/05/setup-a-dnsmasq-equivalent-on-windows-with-acrylic.html).

1. Download and install [Acrylic DNS Proxy](http://mayakron.altervista.org/support/acrylic/Home.htm).

2. Open the GUI:

    ```text
    Startup → Programs → Acrylic DNS Proxy → Acrylic UI
    ```

3. Open Acrylic's hosts file:

    ```text
    File → Open Acrylic Hosts
    ```

4. Add this at the end of Acrylic's hosts file:

    ```text
    127.0.0.1 *.test
    ```

   Save the file. Click yes when it asks to restart the service.

5. Open Windows network configuration and locate current connection's DNS values.

6. Open Acrylic's configuration:

    ```text
    File → Open Acrylic Configuration
    ```

   Replace primary and secondary server addresses with Windows DNS values from step 5:

    ```text
    PrimaryServerAddress=172.20.223.100
    SecondaryServerAddress=172.20.224.100
    ```

   And set the local binding address to 127.0.0.1:
    
    ```text
    LocalIPv4BindingAddress=127.0.0.1
    ```

   Save the file. Click yes when it asks to restart the service.

7. Update Windows DNS values to point to 127.0.0.1 only.
