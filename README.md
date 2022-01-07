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

## JasyptPBEStringDecryptionCLI

```
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by Fernflower decompiler)
//

package org.jasypt.intf.cli;

import java.util.Properties;
import org.jasypt.intf.service.JasyptStatelessService;

public final class JasyptPBEStringDecryptionCLI {
    private static final String[][] VALID_REQUIRED_ARGUMENTS = new String[][]{{"input"}, {"password"}};
    private static final String[][] VALID_OPTIONAL_ARGUMENTS = new String[][]{{"verbose"}, {"algorithm"}, {"keyObtentionIterations"}, {"saltGeneratorClassName"}, {"providerName"}, {"providerClassName"}, {"stringOutputType"}, {"ivGeneratorClassName"}};

    public static void main(String[] args) {
        boolean verbose = CLIUtils.getVerbosity(args);

        try {
            String applicationName = null;
            String[] arguments = null;
            if (args[0] != null && args[0].indexOf("=") == -1) {
                applicationName = args[0];
                arguments = new String[args.length - 1];
                System.arraycopy(args, 1, arguments, 0, args.length - 1);
            } else {
                applicationName = JasyptPBEStringDecryptionCLI.class.getName();
                arguments = args;
            }

            Properties argumentValues = CLIUtils.getArgumentValues(applicationName, arguments, VALID_REQUIRED_ARGUMENTS, VALID_OPTIONAL_ARGUMENTS);
            CLIUtils.showEnvironment(verbose);
            JasyptStatelessService service = new JasyptStatelessService();
            String input = argumentValues.getProperty("input");
            CLIUtils.showArgumentDescription(argumentValues, verbose);
            String result = service.decrypt(input, argumentValues.getProperty("password"), (String)null, (String)null, argumentValues.getProperty("algorithm"), (String)null, (String)null, argumentValues.getProperty("keyObtentionIterations"), (String)null, (String)null, argumentValues.getProperty("saltGeneratorClassName"), (String)null, (String)null, argumentValues.getProperty("providerName"), (String)null, (String)null, argumentValues.getProperty("providerClassName"), (String)null, (String)null, argumentValues.getProperty("stringOutputType"), (String)null, (String)null, argumentValues.getProperty("ivGeneratorClassName"), (String)null, (String)null);
            CLIUtils.showOutput(result, verbose);
        } catch (Throwable var8) {
            CLIUtils.showError(var8, verbose);
        }

    }

    private JasyptPBEStringDecryptionCLI() {
    }
}

```

#### other 场景下的加密解密

##### PBEWITHHMACSHA512ANDAES_256
```java 
import org.jasypt.encryption.pbe.PooledPBEStringEncryptor;
import org.jasypt.encryption.pbe.config.SimpleStringPBEConfig;

public class JasyptUtil {


    public static String encyptPwd(String password, String value) {
        PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
        encryptor.setConfig(cryptor(password));
        String result = encryptor.encrypt(value);
        return result;
    }

    public static String decyptPwd(String password, String value) {
        PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
        encryptor.setConfig(cryptor(password));
        encryptor.decrypt(value);
        String result = encryptor.decrypt(value);
        return result;
    }

    public static SimpleStringPBEConfig cryptor(String password) {
        SimpleStringPBEConfig config = new SimpleStringPBEConfig();
        config.setPassword(password);
        config.setAlgorithm("PBEWITHHMACSHA512ANDAES_256");
        config.setKeyObtentionIterations("1000");
        config.setPoolSize(1);
        config.setProviderName("SunJCE");
        config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator");
        config.setIvGeneratorClassName("org.jasypt.iv.RandomIvGenerator");
        config.setStringOutputType("base64");
        return config;
    }

    public static void main(String[] args) {
        String key = "jas502n";
        String rawPassword = "123456";
        // rTv1dSH1yEVRC6ztDqTEGR8Gd35wrRwERoJivHq3sChy1l6E+Sgu24M1FpXH+Cfd
        System.out.println(encyptPwd(key, rawPassword));

        System.out.println(decyptPwd(key,"rTv1dSH1yEVRC6ztDqTEGR8Gd35wrRwERoJivHq3sChy1l6E+Sgu24M1FpXH+Cfd"));
       }
}

```

输出结果：
```java

PYqKC1KBDiMBfV0cS+SFNM5X/7mOh9EWVKDVGA8Mpi2kvdE7b6n8kr+5JijIi6NH
123456
```



## online decrypt

https://www.devglan.com/online-tools/jasypt-online-encryption-decryption
