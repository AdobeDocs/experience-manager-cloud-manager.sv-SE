---
title: Konfigurera ditt projekt
description: Lär dig hur du konfigurerar ditt projekt så att du kan hantera och driftsätta det med Cloud Manager.
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: 984269e5fe70913644d26e759fa21ccea0536bf4
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---


# Konfigurera ditt projekt {#setting-up-your-project}

Lär dig hur du konfigurerar ditt projekt så att du kan hantera och driftsätta det med Cloud Manager.

## Redigera befintliga projekt {#modifying-project-setup-details}

Befintliga AEM måste följa vissa grundläggande regler så att de kan byggas och driftsättas med Cloud Manager.

* Projekt måste byggas med Apache Maven.
* Det måste finnas en `pom.xml`-fil i Git-databasens rot.
   * Den här `pom.xml`-filen kan referera till så många undermoduler (som i sin tur kan ha andra undermoduler) som behövs.
   * Du kan lägga till referenser till ytterligare Maven-artefaktdatabaser i dina `pom.xml`-filer.
   * Åtkomst till [lösenordsskyddade artefaktdatabaser](#password-protected-maven-repositories) stöds vid konfigurering. Åtkomst till nätverksskyddade artefaktdatabaser stöds dock inte.
* Distribuerbara innehållspaket upptäcks genom att söka efter ZIP-filer i innehållspaketet som finns i en katalog med namnet `target`.
   * Ett valfritt antal undermoduler kan producera innehållspaket.
* Distribuerbara Dispatcher-artefakter upptäcks genom att söka efter `zip` filer som innehåller underkataloger till `target` med namnen `conf` och `conf.d`.
* Om det finns mer än ett innehållspaket är det inte säkert att paketdistributioner ordnas.
* Om en viss ordning behövs kan innehållspaketets beroenden användas för att definiera ordningen.
* Paket kan [hoppas över](#skipping-content-packages) från distributionen.

## Aktivera Maven-profiler i Cloud Manager {#activating-maven-profiles-in-cloud-manager}

I vissa begränsade fall kan du behöva ändra din byggprocess något när den körs i Cloud Manager jämfört med när den körs på arbetsstationer för utvecklare. I dessa fall kan [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) användas för att definiera hur bygget ska vara olika i olika miljöer, inklusive Cloud Manager.

Aktivering av en Maven-profil i Cloud Manager-byggmiljön bör göras genom att söka efter `CM_BUILD` [miljövariabel](/help/getting-started/build-environment.md#environment-variables). Omvänt bör en profil som endast är avsedd att användas utanför Cloud Manager byggmiljö göras genom att man söker efter denna variabel som saknas.

Om du till exempel bara vill visa ett enkelt meddelande när bygget körs i Cloud Manager gör du följande:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Om du vill testa den här profilen på en arbetsstation för utvecklare kan du antingen aktivera den på kommandoraden (med `-PcmBuild`) eller i den integrerade utvecklingsmiljön (IDE).

Om du bara vill få ut ett enkelt meddelande när bygget körs utanför Cloud Manager gör du följande:

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## Stöd för lösenordsskyddade Maven-arkiv {#password-protected-maven-repositories}

Artefakter från lösenordsskyddade Maven-databaser bör användas med försiktighet eftersom kod som distribueras på det här sättet inte är helt underkastad de kvalitetskontroller som Cloud Manager kvalitetsportar kräver. Adobe rekommenderar även att du distribuerar Java-källorna och hela projektets källkod tillsammans med binärfilen.

>[!TIP]
>
>Artefakter från lösenordsskyddade Maven-databaser bör endast användas i sällsynta fall och för kod som inte är knuten till AEM.

Om du vill använda en lösenordsskyddad Maven-databas från Cloud Manager anger du lösenordet (och eventuellt användarnamnet) som en hemlig [förloppsvariabel](/help/getting-started/build-environment.md#pipeline-variables) och refererar sedan till hemligheten i en fil med namnet `.cloudmanager/maven/settings.xml` i Git-databasen. Den här filen följer [Maven Settings File](https://maven.apache.org/settings.html) -schemat.

När Cloud Manager-byggprocessen startar sammanfogas elementet `<servers>` i den här filen med standardfilen `settings.xml` från Cloud Manager. Anpassade servrar ska inte använda server-ID:n som börjar med `adobe` och `cloud-manager`. Sådana ID:n betraktas som reserverade. Cloud Manager speglar endast de server-ID:n som matchar ett av de angivna prefixen eller standard-ID:t `central`.

När den här filen är på plats refereras server-ID:t inifrån ett `<repository>`- och/eller `<pluginRepository>` -element i `pom.xml`-filen. I allmänhet finns dessa `<repository>`- och/eller `<pluginRepository>`-element i en [Cloud Manager-specifik profil](#activating-maven-profiles-in-cloud-manager), även om det inte är absolut nödvändigt.

Anta till exempel att databasen är på `https://repository.myco.com/maven2`, att användarnamnet som Cloud Manager ska använda är `cloudmanager` och att lösenordet är `secretword`.

Först anger du lösenordet som en hemlighet i pipeline:

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword
```

Referera sedan till följande från filen `.cloudmanager/maven/settings.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

Och referera slutligen till server-ID:t i filen `pom.xml`:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

### Distribuera källor {#deploying-sources}

Det är en god vana att driftsätta Java-källorna tillsammans med binärfilen i en Maven-databas.

Konfigurera `maven-source-plugin` i ditt projekt:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### Distribuera projektkällor {#deploying-project-sources}

Det är god praxis att driftsätta hela projektkällan tillsammans med binärfilen till en Maven-databas. Om du gör det kan du återskapa den exakta artefakten.

Konfigurera `maven-assembly-plugin` i ditt projekt:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## Hoppa över innehållspaket {#skipping-content-packages}

I Cloud Manager kan byggen producera valfritt antal innehållspaket. Det kan av olika skäl vara önskvärt att skapa ett innehållspaket men inte distribuera det. Den här metoden kan till exempel vara användbar när du skapar innehållspaket enbart för testning eller när ett annat steg i byggprocessen paketerar om dem. Det vill säga som ett underpaket till ett annat paket.

Cloud Manager letar efter egenskapen `cloudManagerTarget` i egenskaperna för det inbyggda innehållspaketet för att hantera de här scenarierna. Om den här egenskapen är inställd på `none` hoppas paketet över och distribueras inte. Mekanismen för att ange den här egenskapen beror på hur innehållspaketet skapas. Med `filevault-maven-plugin` skulle du till exempel konfigurera plugin-programmet så här:

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

Med `content-package-maven-plugin` är den liknande:

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## Bygg återanvändning av felaktigheter {#build-artifact-reuse}

I många fall distribueras samma kod till flera AEM miljöer. När det är möjligt undviker Cloud Manager att återskapa kodbasen när det upptäcker att samma Git-implementering används i flera fullständiga pipeline-körningar.

När en körning startas extraheras den aktuella HEAD-implementeringen för förgreningsflödet. Hash för implementeringen visas i användargränssnittet och via API:t. När byggsteget har slutförts lagras de resulterande artefakterna baserat på den implementeringshashen och kan återanvändas i efterföljande pipeline-körningar.

Paket återanvänds i alla rörledningar om de ingår i samma program. När du söker efter paket som kan återanvändas ignorerar AEM grenar och återanvänder artefakter över grenar.

När en återanvändning sker ersätts stegen för bygg- och kodkvalitet effektivt med resultaten från den ursprungliga körningen. Loggfilen för byggsteget innehåller artefakter och körningsinformation som användes för att skapa dem från början.

Här följer ett exempel på sådana loggutdata.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Loggen för kodkvalitetssteget innehåller liknande information.

### Exempel {#example-reuse}

#### Exempel 1 {#example-1}

Tänk på att ditt program har två utvecklingspipelines:

* Pipeline 1 på grenen `foo`
* Pipeline 2 på gren `bar`

Båda grenarna har samma implementerings-ID.

1. När du kör pipeline 1 skapas paketen normalt.
1. När du sedan kör pipeline 2 återanvänds paket som skapats med pipeline 1.

#### Exempel 2 {#example-2}

Tänk på att ditt program har två grenar: Förgrening `foo` och Förgrening `bar`.

Båda grenarna har samma implementerings-ID.

1. En utvecklingspipeline skapar och kör `foo`.
1. Därefter byggs och körs `bar` av en produktionspipeline.

I det här fallet återanvänds artefakten från `foo` för produktionsflödet eftersom samma implementeringshash identifierades.

### Avanmäl dig {#opting-out}

Om du vill kan återanvändningsbeteendet inaktiveras för specifika pipelines genom att pipeline-variabeln `CM_DISABLE_BUILD_REUSE` anges till `true`. Om variabeln är inställd extraheras fortfarande implementeringshash-värdet. De resulterande artefakterna lagras för senare bruk, men tidigare lagrade artefakter återanvänds inte. Tänk på följande scenario om du vill förstå detta:

1. En ny pipeline skapas.
1. Pipelinen körs (körning nr 1) och den aktuella HEAD-implementeringen är `becdddb`. Körningen är klar och de resulterande artefakterna sparas.
1. Variabeln `CM_DISABLE_BUILD_REUSE` har angetts.
1. Pipelinen körs igen utan att koden ändras. Även om det finns lagrade artefakter som är associerade med `becdddb`, återanvänds de inte på grund av variabeln `CM_DISABLE_BUILD_REUSE`.
1. Koden ändras och pipeline körs. HEAD implementering är nu `f6ac5e6`. Körningen är klar och de resulterande artefakterna sparas.
1. Variabeln `CM_DISABLE_BUILD_REUSE` har tagits bort.
1. Pipelinen körs igen utan att koden ändras. Eftersom det finns lagrade artefakter associerade med `f6ac5e6`, återanvänds dessa artefakter.

### Caveats {#caveats}

* Skapa artefakter återanvänds inte i olika program, oavsett om implementeringshashen är identisk.
* Artefakter återanvänds i samma program även om grenen och/eller pipeline är annorlunda.
* [Versionshantering för Maven](/help/managing-code/maven-project-version.md) ersätter endast projektversionen i produktionspipelines. Om samma implementering används för både utvecklings- och produktionspipeline och utvecklingspipelines körs först, distribueras versionerna till scenen och produktionen oförändrad. I det här fallet skapas dock fortfarande en tagg.
* Om hämtningen av de lagrade artefakterna inte lyckas, körs byggsteget som om inga artefakter lagrades.
* Andra förloppsvariabler än `CM_DISABLE_BUILD_REUSE` beaktas inte när Cloud Manager beslutar att återanvända tidigare skapade byggartefakter.

## Utveckla din kod baserat på bästa praxis {#develop-your-code-based-on-best-practices}

Adobe tekniker och konsultteam har utvecklat en [omfattande uppsättning med bästa praxis för AEM utvecklare](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/implementing/developing/bestpractices/best-practices).
