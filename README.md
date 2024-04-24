<a name="readme-top">

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="https://images.contentstack.io/v3/assets/bltefdd0b53724fa2ce/blt3e2c7bebbae51138/6568a0834c0b9a3624d5582a/logo-tagline-white.svg" alt="Logo" width="300" height="80">
  </a>
</div>
</a>

this tutorial will contain:
* Installing Heartbeat





<!-- ABOUT THE PROJECT -->
## About 
Heartbeat is one of elastic component that check services status periodically we will explain the steps and its featuers




<!-- GETTING STARTED -->
## Getting Started

In this tutorial you need to have linux Fedora please complite the the setup in the link [ElasticSearch tutorial](https://github.com/wildcard-94/ElasticSearch)

we will use the ES and Kibana scripts to install the packages


### Installation

1. Go to observability section and select uptime   
    <p>
    <img width="360" height="320" src="https://i.imgur.com/lc1Fuki.png" >
    </p>

2. select add monitors with heartbeat   
    <p>
    <img width="360" height="320" src="https://imgur.com/TeUwsZ6.png" >
    </p>
    
3. Download heartbeat 
   ```sh
   curl -L -O https://artifacts.elastic.co/downloads/beats/heartbeat/heartbeat-8.2.0-x86_64.rpm
   sudo rpm -vi heartbeat-8.2.0-x86_64.rpm
   ```
4. open and unpin username and password
   ```sh
   sudo nano /etc/heartbeat/heartbeat.yml
   ```

5. add cert fingerprint 
    <p>
    <img width="360" height="320" src="https://imgur.com/TstXxyH.png" >
    </p>
   ```sh
   ssl.ca_trusted_fingerprint: "<es cert fingerprint>"
   ```
   
6. copy the output of default elastic cert by openssl and paste it in the yml file
   ```sh
   openssl x509 -fingerprint -sha256 -noout -in /etc/elasticsearch/certs/http_ca.crt | awk --field-separator="=" '{print $2}' | sed 's/://g'
   ```
7. or you can skip and use the certificate authorities  
   ```sh
   ssl.certificate_authorities: ["/etc/elasticsearch/certs/http_ca.crt"]
   ```
8. configure http monitor 
    <p>
    <img width="360" height="220" src="https://imgur.com/5weblck.png" >
    </p>
   
9. Check setup and reachability
   ```sh
   cd /usr/share/heartbeat/
   sudo cp /etc/heartbeat/heartbeat.yml .
   sudo ./bin/heartbeat test config
   sudo ./bin/heartbeat setup
   ```
   
    <p>
    <img width="360" height="150" src="https://imgur.com/JMGUs8V.png" >
    </p>

10. Run heartbeat script
   ```sh
   sudo systemctl start heartbeat-elastic
   ```
11. configure http monitor 
    <p>
    <img width="600" height="220" src="https://imgur.com/vwVDiex.png" >
    </p>





## References

* [Heartbeat quick start 8.2](https://www.elastic.co/guide/en/beats/heartbeat/8.2/heartbeat-installation-configuration.html)
* [Heartbeat quick start 8.13](https://www.elastic.co/guide/en/beats/heartbeat/8.13/heartbeat-installation-configuration.html)


<p align="right">(<a href="#readme-top">back to top</a>)</p>



