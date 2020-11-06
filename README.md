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

## online decrypt

https://www.devglan.com/online-tools/jasypt-online-encryption-decryption
