# MT Connect

- [Getting started with MT Connect](./GettingStartedWithMTConnect.pdf)
- [Presentation about MT Connect](./PresentationAboutMTConnect.pdf)
- [Remote MT server](https://smstestbed.nist.gov/vds/sample?count=1000)
- [Haas documentation about MT Connect](https://www.haascnc.com/service/troubleshooting-and-how-to/how-to/machine-data-collection---ngc.html)
- [Preparing MT connect simulator locally](https://github.com/mtconnect/cppagent/issues/115)

Getting data with curl from remote server:

```bash
curl https://smstestbed.nist.gov/vds/sample?count=10
```

[How to integrate RapidXML with your C++ app](https://cpp0x.pl/artykuly/Inne-artykuly/C++-Obsluga-plikow-XML-biblioteka-RapidXML/50)

## About MT connect

![About MT connect](./basically_about_mt_connect.png)

To get data from MT server you should send a HTTP/HTTPS requests.

There are 4 kinds of XML responses:

- Devices
    - `vds` - name of device
    - `probe` - request type which get metadata
    - https://smstestbed.nist.gov/vds/probe
- Streams
    - Real-time stream of most current value for each data item: https://smstestbed.nist.gov/vds/current
    - Time series of most recent values collected for each data item: https://smstestbed.nist.gov/vds/sample
- Assets
    - Retrieve information on mobile assets
- Error
    - Returned when an error occurs that prevents further processing

More about that in `Getting started with MT Connect`.
