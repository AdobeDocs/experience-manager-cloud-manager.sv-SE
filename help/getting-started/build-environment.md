---
title: Byggmiljön
description: Läs om den speciella byggmiljö som Cloud Manager-användare kan använda för att skapa och testa din kod.
exl-id: b3543320-66d4-4358-8aba-e9bdde00d976
source-git-commit: fb3c2b3450cfbbd402e9e0635b7ae1bd71ce0501
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---


# Byggmiljön {#build-environment}

Läs om den speciella byggmiljö som Cloud Manager-användare kan använda för att skapa och testa din kod.

## Miljöinformation {#details}

Cloud Manager byggmiljöer har följande attribut.

* Byggmiljön är Linux-baserad och kommer från Ubuntu 2.04.
* Apache Maven 3.9.4 är installerad.
   * Adobe rekommenderar att användare [uppdaterar sina Maven-databaser så att de använder HTTPS i stället för HTTP](#https-maven).
* Java-versionerna är Oracle JDK 8u401 och Oracle JDK 11.0.22.
   * `/usr/lib/jvm/jdk1.8.0_401`
   * `/usr/lib/jvm/jdk-11.0.22`
* Miljövariabeln `JAVA_HOME` är som standard inställd på `/usr/lib/jvm/jdk1.8.0_401`, som innehåller Oracle JDK 8u401. Mer information finns i avsnittet [Alternate Maven Execution JDK Version](#alternate-maven).
* Det finns ytterligare systempaket installerade som är nödvändiga.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Andra paket kan installeras vid byggtillfället enligt beskrivningen i avsnittet [Installera ytterligare systempaket](#installing-additional-system-packages).
* Varje bygge görs i en riktig miljö. Byggbehållaren behåller inte något läge mellan körningar.
* Maven drivs med följande tre kommandon:
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven har konfigurerats på systemnivå med en `settings.xml`-fil, som automatiskt inkluderar den offentliga Adobe-artefaktdatabasen med en profil med namnet `adobe-public`. Mer information finns i [Adobe gemensamma Maven-databas](https://repo1.maven.org/).
* Node.js 18 är tillgängligt för [frontendpipelines](/help/overview/ci-cd-pipelines.md).

>[!NOTE]
>
>Även om Cloud Manager inte definierar någon specifik version av `jacoco-maven-plugin` måste den version som används vara minst `0.7.5.201505241946`.

>[!TIP]
>
>Se följande ytterligare resurser för att lära dig hur du använder Cloud Manager API:er:
>
>* [aio-cli-plugin-cloudManager](https://github.com/adobe/aio-cli-plugin-cloudmanager)
>* [Skapar en API-integrering](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)
>* [API-behörigheter](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)

## HTTPS Maven-databaser {#https-maven}

Cloud Manager [2023.10.0](/help/release-notes/2023/2023-10-0.md) påbörjade en rullande uppdatering av byggmiljön (som slutfördes med version 2023.12.0), som innehöll en uppdatering till Maven 3.8.8. En betydande förändring som introducerades i Maven 3.8.1 var en säkerhetsförbättring som syftar till att minska potentiella sårbarheter. Maven inaktiverar nu alla osäkra `http://*`-speglar som standard, vilket beskrivs i [versionsinformationen för Maven](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Som ett resultat av den här säkerhetsförbättringen kan vissa användare råka ut för problem under byggfasen, särskilt när artefakter hämtas från Maven-databaser som använder osäkra HTTP-anslutningar.

För att få en smidig upplevelse med den uppdaterade versionen rekommenderar Adobe att användare uppdaterar sina Maven-databaser så att HTTPS används istället för HTTP. Denna justering är anpassad efter branschens växande övergång till säkra kommunikationsprotokoll och hjälper till att upprätthålla en säker och tillförlitlig byggprocess.

## Använda en specifik Java-version {#using-java-version}

Som standard används JDK för projekt som byggts med Cloud Manager. Kunder som vill använda en alternativ JDK har två alternativ.

* [Maven Toolchains](#maven-toolchains)
* [Välja en alternativ JDK-version för hela körningsprocessen för Maven](#alternate-maven)

### Maven Toolchains {#maven-toolchains}

Med plugin-programmet [Maven Toolchains](https://maven.apache.org/plugins/maven-toolchains-plugin/) kan projekt välja en specifik JDK (eller verktygskedja) som ska användas i kontexten för verktygskedjemedvetna Maven-plugin. Den här processen görs i projektets `pom.xml`-fil genom att ange en leverantör och ett versionsvärde. Ett exempelavsnitt i filen `pom.xml` är följande:

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

Den här processen gör att alla verktygskedjedåliga Maven-plugin-program använder Oracle JDK, version 11.

När du använder den här metoden körs Maven fortfarande med standardvariabeln JDK (Oracle 8) och miljövariabeln `JAVA_HOME` ändras inte. Kontroll eller genomförande av Java-versionen via plugin-program som [Apache Maven Enforcer ](https://maven.apache.org/enforcer/maven-enforcer-plugin/) fungerar därför inte och sådana plugin-program får inte användas.

De aktuella kombinationerna av leverantör/version är:

| Leverantör | Version |
|---|---|
| Oracle | 1,8 |
| Oracle | 1,11 |
| Oracle | 11 |
| Sun | 1,8 |
| Sun | 1,11 |
| Sun | 11 |

>[!NOTE]
>
>Från och med april 2022 kommer Oracle JDK att bli standard-JDK för utveckling och drift av AEM-program. Cloud Manager byggprocess växlar automatiskt till att använda Oracle JDK, även om ett alternativt alternativ uttryckligen väljs i Maven-verktygskedjan. Mer information finns i versionsinformationen för [april](/help/release-notes/2022/2022-4-0.md).

### JDK-version för körning av alternativ Maven {#alternate-maven}

Du kan också välja Oracle 8 eller Oracle 11 som JDK för hela Maven-exekveringen. Till skillnad från alternativen för verktygskedjor ändras det JDK som används för alla plugin-program, såvida inte konfigurationen för verktygskedjor också är inställd. I så fall används fortfarande konfigurationen för verktygskedjor för Maven-plugin-program som är medvetna för verktygskedjor. Det innebär att kontroll och genomförande av Java-versionen med plugin-programmet [Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) fungerar.

Om du vill göra det skapar du en fil med namnet `.cloudmanager/java-version` i Git-databasgrenen som används av pipeline. Den här filen kan ha antingen innehållet `11` eller `8`. Alla andra värden ignoreras. Om `11` anges används Oracle 11 och miljövariabeln `JAVA_HOME` ställs in på `/usr/lib/jvm/jdk-11.0.22`. Om `8` anges används Oracle 8 och miljövariabeln `JAVA_HOME` ställs in på `/usr/lib/jvm/jdk1.8.0_401`.

## Miljövariabler {#environment-variables}

### Standardmiljövariabler {#standard-environ-variables}

I vissa fall kan det vara nödvändigt att variera byggprocessen baserat på information om programmet eller pipeline.

Om du till exempel använder ett verktyg som Glup för JavaScript-miniatyrbilder kan du föredra olika nivåer för utveckling jämfört med staging- och produktionsmiljöer.

Som stöd för detta lägger Cloud Manager till standardmiljövariabler i byggbehållaren för varje körning.

| Variabelnamn | Beskrivning |
|---|---|
| `CM_BUILD` | Alltid inställd på `true` |
| `BRANCH` | Den konfigurerade grenen för körningen |
| `CM_PIPELINE_ID` | Den numeriska pipeline-identifieraren |
| `CM_PIPELINE_NAME` | Pipeline-namnet |
| `CM_PROGRAM_ID` | Den numeriska programidentifieraren |
| `CM_PROGRAM_NAME` | Programnamnet |
| `ARTIFACTS_VERSION` | För en stagnings- eller produktionsprocess genereras den syntetiska versionen av Cloud Manager |

### Variabel tillgänglighet för standardmiljö {#availability}

Standardmiljövariabler kan användas på flera ställen.

#### Skapa, förhandsgranska och publicera miljöer {#author-preview-publish}

Både vanliga miljövariabler och hemligheter kan användas i redigerings-, förhandsgransknings- och publiceringsmiljöer.

#### Dispatcher {#dispatcher}

Endast reguljära miljövariabler kan användas med [Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/dispatcher). Hemligheter kan inte användas.

Miljövariabler kan dock inte användas i `IfDefine`-direktiv.

>[!TIP]
>
>Verifiera din användning av miljövariabler med [Dispatcher lokalt](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools) innan du distribuerar.

#### OSGi-konfigurationer {#osgi}

Både vanliga miljövariabler och hemligheter kan användas i [OSGi-konfigurationer](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi).

### Pipeline-variabler {#pipeline-variables}

I vissa fall kan din byggprocess vara beroende av specifika konfigurationsvariabler som skulle vara olämpliga att placera i Git-databasen eller som behöver variera mellan olika pipeline-körningar som använder samma gren.

Cloud Manager tillåter att dessa variabler konfigureras via Cloud Manager API eller Cloud Manager CLI per pipeline. Variabler kan lagras som antingen oformaterad text eller krypteras i vila. I båda fallen görs variabler tillgängliga i byggmiljön som en miljövariabel, som sedan kan refereras inifrån filen `pom.xml` eller andra byggskript.

Om du vill ange en variabel med hjälp av CLI kör du ett kommando som liknar följande.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Aktuella variabler kan listas med ett kommando som liknar följande.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

Variabler måste följa vissa begränsningar.

* Variabelnamn får endast innehålla alfanumeriska tecken och understreck (`_`).
   * Namnen ska vara versaler.
* Det finns en gräns på 200 variabler per pipeline.
* Varje namn får innehålla högst 100 tecken.
* Varje strängvärde måste innehålla färre än 2 048 tecken.
* Varje `secretString`-värde måste innehålla färre än 500 tecken.

När de används i en Maven `pom.xml`-fil är det vanligtvis praktiskt att mappa dessa variabler till Maven-egenskaper med en syntax som liknar den nedan.

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

För att vissa byggen ska fungera fullt ut krävs att ytterligare systempaket installeras. Ett bygge kan till exempel anropa ett Python- eller Ruby-skript och därför måste ha en lämplig språktolk installerad. Det här scenariot kan utföras genom att anropa [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) för att anropa APT. Den här exekveringen bör normalt omslutas av en Cloud Manager-specifik Maven-profil. Om du till exempel vill installera Python kan du göra följande:

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

Den här tekniken kan även användas för att installera språkspecifika paket. Det innebär att `gem` används för RubyGems eller `pip` för Python-paket.

>[!NOTE]
>
>Om du installerar ett systempaket på det här sättet installeras det inte i den körningsmiljö som används för att köra Adobe Experience Manager. Kontakta din Adobe-representant om du behöver ett systempaket som är installerat i AEM-miljön.
