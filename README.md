# jasypt Decrypt Encrypt 


## e.g. 


`application.yml`

```
  #mysql数据库配置
  datasource:
    url: jdbc:mysql://127.0.0.1:3306/secert?useServerPrepStmts=true
    username: root
    password: ENC(wQ2RWioogVIXRdfTipVT6UW/J0Waxa0n)
    driver-class-name: com.mysql.cj.jdbc.Driver
```

`ENC(wQ2RWioogVIXRdfTipVT6UW/J0Waxa0n)` need `jas502n` to Decrypt

## Encrypt

```
╰─$ java -cp jasypt-1.9.3.jar org.jasypt.intf.cli.JasyptPBEStringEncryptionCLI input="ThisIsMySecert" password="jas502n" algorithm=PBEWithMD5AndDES

----ENVIRONMENT-----------------

Runtime: Oracle Corporation Java HotSpot(TM) 64-Bit Server VM 25.60-b23



----ARGUMENTS-------------------

algorithm: PBEWithMD5AndDES
input: ThisIsMySecert
password: jas502n



----OUTPUT----------------------

wQ2RWioogVIXRdfTipVT6UW/J0Waxa0n
```

## Decrypt

```
╰─$ java -cp jasypt-1.9.3.jar org.jasypt.intf.cli.JasyptPBEStringDecryptionCLI input="wQ2RWioogVIXRdfTipVT6UW/J0Waxa0n" password="jas502n" algorithm=PBEWithMD5AndDES

----ENVIRONMENT-----------------

Runtime: Oracle Corporation Java HotSpot(TM) 64-Bit Server VM 25.60-b23



----ARGUMENTS-------------------

algorithm: PBEWithMD5AndDES
input: wQ2RWioogVIXRdfTipVT6UW/J0Waxa0n
password: jas502n



----OUTPUT----------------------

ThisIsMySecert

```
