---
title: Förstå byggmiljön
description: Följ den här sidan om du vill veta mer om miljöer
feature: Miljöer
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# Förstå byggmiljön {#build-environment-details}

Cloud Manager bygger och testar koden med en specialiserad byggmiljö. Den här miljön har följande attribut:

* Byggmiljön är Linux-baserad och kommer från Ubuntu 18.04.
* Apache Maven 3.6.0 är installerad.
* De Java-versioner som är installerade är Oraclena JDK 8u202, Azul Zulu 8u292, Oracle JDK 11.0.2 och Azul Zulu 11.0.11.
* Det finns ytterligare systempaket installerade som är nödvändiga:

   * bzip2
   * uppzip
   * libpng
   * imagemagick
   * grafikSnabb

* Andra paket kan installeras vid byggtillfället enligt beskrivningen [nedan](#installing-additional-system-packages).
* Varje bygge görs i en riktig miljö. byggbehållaren behåller inte något läge mellan körningar.
* Maven körs alltid med dessa tre kommandon:

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`

* Maven konfigureras på systemnivå med filen settings.xml som automatiskt inkluderar databasen Adobe **Artifact** med en profil med namnet `adobe-public`.
Mer information finns i [Adobe Public Maven Repository](https://repo.adobe.com/).

>[!NOTE]
>Även om Cloud Manager inte definierar en specifik version av `jacoco-maven-plugin` måste den version som används vara minst `0.7.5.201505241946`.


>[!NOTE]
>Mer information om hur du använder API:er för Cloud Manager finns i följande extraresurser:
> * [aio-cli-plugin-cloud-manager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [Skapa en API-integrering](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md)
>* [API-behörigheter](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)


## Använda en specifik Java-version {#using-java-version}

Som standard byggs projekt av Cloud Managers byggprocess med Oracle 8 JDK. Kunder som vill använda en alternativ JDK har två alternativ: Maven Toolchains och välj en alternativ JDK-version för hela Maven-exekveringsprocessen.

### Maven Toolchains {#maven-toolchains}

Med [Plugin-programmet Maven Toolchains](https://maven.apache.org/plugins/maven-toolchains-plugin/) kan projekt välja en viss JDK (eller *verktygskedja*) som ska användas i samband med verktygsfältsanpassade Maven-pluginer. Detta görs i projektets `pom.xml`-fil genom att ange en leverantör och ett versionsvärde. Ett exempelavsnitt i `pom.xml`-filen är:

```xml
        <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

Detta gör att alla verktygskedjedåliga Maven-plugin-program använder Oraclet JDK, version 11.

När du använder den här metoden körs Maven fortfarande med JDK-standardinställningen (Oracle 8). Kontroll eller genomförande av Java-versionen via plugin-program som [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) fungerar inte och sådana plugin-program får inte användas.

De aktuella kombinationerna av leverantör/version är:

* oracle 1.8
* oracle 1.11
* oracle 11
* sol 1.8
* sol 1.11
* sol 11
* azul 1.8
* azul 1.11
* azul 8

### Alternate Maven Execution JDK Version {#alternate-maven}

Det går också att välja Azul 8 eller Azul 11 som JDK för hela Maven-exekveringen. Till skillnad från alternativen för verktygskedjor ändras det JDK som används för alla plugin-program, såvida inte konfigurationen för verktygskedjor också anges. I så fall tillämpas fortfarande konfigurationen för verktygskedjor för Maven-plugin-program som är medvetna om verktygskedjor. Därför kommer kontroll och genomförande av Java-versionen med [Apache Maven Enforcer Plugin](https://maven.apache.org/enforcer/maven-enforcer-plugin/) att fungera.

Det gör du genom att skapa en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipeline. Den här filen kan ha antingen innehållet 11 eller 8. Alla andra värden ignoreras. Om 11 anges används Azul 11. Om 8 anges används Azul 8.

>[!NOTE]
>I en framtida version av Cloud Manager, som för närvarande beräknas vara i oktober 2021, ändras standard-JDK och standardvärdet är Azul 11. Projekt som inte är kompatibla med Java 11 bör skapa den här filen med innehåll 8 så snart som möjligt för att vara säkra på att de inte påverkas av den här växeln.


## Miljövariabler {#environment-variables}

### Standardmiljövariabler {#standard-environ-variables}

I vissa fall tycker kunderna att det är nödvändigt att variera byggprocessen baserat på information om programmet eller pipeline.

Om JavaScript-minifiering under byggtid utförs, till exempel med hjälp av ett verktyg som Glup, kan det finnas en önskan att använda en annan Minification-nivå när du skapar för en utvecklingsmiljö i stället för att bygga för scenen och produktionen.

Som stöd för detta lägger Cloud Manager till dessa standardmiljövariabler i byggbehållaren för varje körning.

| **Variabelnamn** | **Definition** |
|---|---|
| CM_BUILD | Alltid inställd på &quot;true&quot; |
| BRANSCHER | Den konfigurerade grenen för körningen |
| CM_PIPELINE_ID | Den numeriska pipeline-identifieraren |
| CM_PIPELINE_NAME | Pipeline-namnet |
| CM_PROGRAM_ID | Den numeriska programidentifieraren |
| CM_PROGRAM_NAME | Programnamnet |
| ARTIFACTS_VERSION | Den syntetiska versionen som genererats av Cloud Manager för en fas eller produktionsprocess |

### Rörledningsvariabler {#pipeline-variables}

I vissa fall kan en kunds byggprocess vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen eller som behöver variera mellan olika pipeline-körningar som använder samma gren.

Med Cloud Manager kan dessa variabler konfigureras via Cloud Manager API eller Cloud Manager CLI per pipeline. Variabler kan lagras som antingen ren text eller krypteras i vila. I båda fallen görs variabler tillgängliga i byggmiljön som en miljövariabel som sedan kan refereras inifrån `pom.xml`-filen eller andra byggskript.

Om du vill ange en variabel med hjälp av CLI kör du ett kommando som:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

Aktuella variabler kan listas:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

Variabelnamn får endast innehålla alfanumeriska tecken och understreck (_). Namnen ska vara versaler. Det finns en gräns på 200 variabler per pipeline, där varje namn måste innehålla mindre än 100 tecken och varje värde måste vara mindre än 2 048 tecken för strängtypsvariabler och 500 tecken för värden av typen secretsString.

När de används i en `Maven pom.xml`-fil är det vanligtvis praktiskt att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den här:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```


## Installera ytterligare systempaket {#installing-additional-system-packages}

Vissa byggen kräver att ytterligare systempaket installeras för att fungera helt. Ett bygge kan till exempel anropa ett Python- eller ruby-skript och därför måste ha en lämplig språktolk installerad. Detta kan du göra genom att anropa [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) för att anropa APT. Den här exekveringen bör normalt omslutas av en molnhanterarspecifik Maven-profil. Så här installerar du python:

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Samma teknik kan användas för att installera språkspecifika paket, t.ex. med `gem` för RubyGems eller `pip` för Python-paket.

>[!NOTE]
>Om du installerar ett systempaket på det här sättet installeras det **inte** i körningsmiljön som används för att köra Adobe Experience Manager. Om du behöver ett systempaket som är installerat i AEM ska du kontakta Adobe.
