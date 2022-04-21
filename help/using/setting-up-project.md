---
title: Konfigurera projektet
description: Följ den här sidan för att lära dig hur du konfigurerar ett projekt
feature: Getting Started, Production Programs
exl-id: ed994daf-0195-485a-a8b1-87796bc013fa
source-git-commit: fd1a72f2fd3b3e3789fcb38a8d4a9585293ced50
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 4%

---

# Konfigurera projektet {#setting-up-your-project}

## Ändra projektinställningsinformation {#modifying-project-setup-details}

In order to be built and deployed successfully with Cloud Manager, existing AEM projects need to adhere to some basic rules:

* Projekt måste byggas med Apache Maven.
* There must be a *pom.xml* file in the root of the Git repository. Detta *pom.xml* filen kan referera till så många undermoduler (som i sin tur kan ha andra undermoduler osv.) vid behov.

* Du kan lägga till referenser till ytterligare Maven-artefaktdatabaser i dina *pom.xml* filer. Access to [password-protected artifact repositories](#password-protected-maven-repositories) is supported when configured. Åtkomst till nätverksskyddade artefaktdatabaser stöds dock inte.
* Distribuerbara innehållspaket identifieras genom sökning efter innehållspaket *zip* filer som finns i en katalog med namnet *target*. Any number of sub-modules may produce content packages.

* Distribuerbara Dispatcher-artefakter upptäcks vid sökning efter *zip* filer (igen, i en katalog med namnet *target*) som har kataloger namngivna *conf* och *conf.d*.

* Om det finns mer än ett innehållspaket är det inte säkert att paketdistributioner ordnas. Om en viss ordning behövs kan innehållspaketets beroenden användas för att definiera ordningen. Paket kan vara [överhoppad](#skipping-content-packages) från driftsättning.


## Aktivera Maven-profiler i Cloud Manager {#activating-maven-profiles-in-cloud-manager}

I vissa begränsade fall kan du behöva ändra din byggprocess något när du kör i Cloud Manager i stället för när den körs på arbetsstationer för utvecklare. For these cases, [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) can be used to define how the build should be different in different environments, including Cloud Manager.

Aktivering av en Maven-profil i Cloud Managers byggmiljö bör göras genom att söka efter miljövariabeln CM_BUILD som beskrivs ovan. Omvänt bör en profil som bara är avsedd att användas utanför Cloud Manager-byggmiljön göras genom att leta efter denna variabel som saknas.

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
>To test this profile on a developer workstation, you can either enable it on the command line (with `-PcmBuild`) or in your Integrated Development Environment (IDE).

Om du bara vill få ut ett enkelt meddelande när bygget körs utanför Cloud Manager gör du det här:

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

## Lösenordsskyddat databasstöd för Maven {#password-protected-maven-repositories}

>[!NOTE]
>Artefakter från en lösenordsskyddad Maven-databas bör endast användas med försiktighet eftersom kod som distribueras via den här mekanismen för närvarande inte kan köras med alla kvalitetsregler som implementerats i Cloud Managers Quality Gates. Därför bör det endast användas i sällsynta fall och för kod som inte är knuten till AEM. Du bör också distribuera Java-källorna samt hela projektets källkod tillsammans med binärfilen.

Om du vill använda en lösenordsskyddad Maven-databas från Cloud Manager anger du lösenordet (och eventuellt användarnamnet) som en hemlighet [Rörledningsvariabel](/help/using/build-environment-details.md#pipeline-variables) referera sedan till hemligheten i en fil med namnet `.cloudmanager/maven/settings.xml` i Git-databasen. Filen följer [Maven Settings-fil](https://maven.apache.org/settings.html) schema. When the Cloud Manager build process starts, the `<servers>` element in this file will be merged into the default `settings.xml` file provided by Cloud Manager. Server IDs starting with `adobe` and `cloud-manager` are considered reserved and should not be used by custom servers. Server-ID **not** matchar något av dessa prefix eller standard-ID `central` kommer aldrig att speglas av Cloud Manager. När den här filen är på plats refereras server-ID:t inifrån en `<repository>` och/eller `<pluginRepository>` -element inuti `pom.xml` -fil. I allmänhet gäller följande `<repository>` och/eller `<pluginRepository>` -element finns inuti en [Cloud Manager-specifik profil](#activating-maven-profiles-in-cloud-manager)även om det inte är absolut nödvändigt.

As an example, let&#39;s say that the repository is at https://repository.myco.com/maven2, the username Cloud Manager should use is `cloudmanager` and the password is `secretword`.

Först anger du lösenordet som en hemlighet i pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Referera sedan det här från `.cloudmanager/maven/settings.xml` fil:

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

And finally reference the server id inside the `pom.xml` file:

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

Konfigurera maven-source-plugin i ditt projekt:

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

### Deploying Project Sources {#deploying-project-sources}

It is a good practice to deploy the whole project source alongside with the binary to a Maven repository - this allows as to rebuild the exact artifact.

Configure the maven-assembly-plugin in your project:

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

## Hoppar över innehållspaket {#skipping-content-packages}

I Cloud Manager kan byggen producera valfritt antal innehållspaket.
Det kan av olika skäl vara önskvärt att skapa ett innehållspaket men inte distribuera det. Detta kan till exempel vara användbart när du skapar innehållspaket som bara används för testning eller som paketeras om med ett annat steg i byggprocessen, det vill säga som ett underpaket till ett annat paket.

För att hantera dessa scenarier söker Cloud Manager efter egenskapen ***cloudManagerTarget*** i egenskaperna för de byggda innehållspaketen. Om den här egenskapen är inställd på ”ingen” hoppas paketet över och driftsätts inte. Mekanismen för hur den här egenskapen anges beror på hur innehållspaketet skapas. Med till exempel filevault-maven-plugin konfigurerar du plugin-programmet så här:

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

Med content-package-maven-plugin är den ungefär så här:

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

In many cases, the same code is deployed to multiple AEM environments. Om det är möjligt kommer Cloud Manager att undvika att återskapa kodbasen när det upptäcker att samma Git-implementering används i flera fullständiga pipeline-körningar.

When an execution is started, the current HEAD commit for the branch pipeline is extracted. The commit hash is visible in the UI and via the API. When the build step completes successfully, the resulting artifacts are stored based on that commit hash and may be reused in subsequent pipeline executions.

Paket återanvänds i alla rörledningar om de ingår i samma program. När du söker efter paket som kan återanvändas ignorerar AEM grenar och återanvänder artefakter över grenar.

När en återanvändning sker ersätts stegen för bygg- och kodkvalitet effektivt med resultaten från den ursprungliga körningen. The log file for the build step will list the artifacts and the execution information which was used to build them originally.

The following is an example of such log output.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Loggen för kodkvalitetssteget innehåller liknande information.

### Exempel {#example-reuse}

#### Example 1 {#example-1}

Tänk på att ditt program har två utvecklingspipelines:

* Pipeline 1 on branch `foo`
* Pipeline 2 on branch `bar`

Båda grenarna har samma implementerings-ID.

1. Running Pipeline 1 first will build the packages normally.
1. När du sedan kör Pipeline 2 återanvänds paket som skapats med Pipeline 1.

#### Example 2 {#example-2}

Consider that your program has two branches:

* Branch `foo`
* Gren `bar`

Both branches have the same commit ID.

1. En utvecklingsprocess bygger och verkställer `foo`.
1. Därefter byggs och körs en produktionsprocess `bar`.

I det här fallet är artefakten från `foo` kommer att återanvändas för produktionsflödet eftersom samma implementeringshash identifierades.

### Avmarkera {#opting-out}

Om du vill kan återanvändningsbeteendet inaktiveras för specifika rörledningar genom att ange rörledningsvariabeln `CM_DISABLE_BUILD_REUSE` till `true`. Om den här variabeln är inställd extraheras fortfarande implementeringshashen och de resulterande artefakterna lagras för senare användning, men eventuella tidigare lagrade artefakter återanvänds inte. Tänk på följande scenario om du vill förstå det här beteendet.

1. En ny pipeline skapas.
1. Pipelinen körs (exekvering nr 1) och den aktuella implementeringen i HEAD är `becdddb`. Körningen är klar och de resulterande artefakterna sparas.
1. The `CM_DISABLE_BUILD_REUSE` variabeln är inställd.
1. Pipelinen körs igen utan att koden ändras. Även om lagrade artefakter är associerade med `becdddb`, används de inte på grund av `CM_DISABLE_BUILD_REUSE` variabel.
1. Koden ändras och pipeline körs. HEAD har bekräftat `f6ac5e6`. Körningen är klar och de resulterande artefakterna sparas.
1. The `CM_DISABLE_BUILD_REUSE` variable is deleted.
1. The pipeline is re-executed without changing the code. Eftersom lagrade artefakter är associerade med `f6ac5e6`, återanvänds dessa artefakter.

### Caveats {#caveats}

* Build artifacts are not reused across different programs, regardless if the commit hash is identical.
* Artefakter återanvänds i samma program även om grenen och/eller pipeline är annorlunda.
* [Hantering av versioner av Maven](/help/using/activating-maven-project.md) ersätter endast projektversionen i produktionspipelines. Om samma implementering används både för en körning av en utvecklingsdistribution och en körning av en produktionspipeline och utvecklingsdistributionen körs först, distribueras versionerna till fas och produktion utan att ändras. I det här fallet kommer dock en tagg fortfarande att skapas.
* Om hämtningen av de lagrade artefakterna inte lyckas kommer byggsteget att utföras som om inga artefakter hade lagrats.
* Pipeline variables other than `CM_DISABLE_BUILD_REUSE` are not considered when Cloud Manager decides to reuse previously created build artifacts.

## Utveckla din kod baserat på bästa praxis {#develop-your-code-based-on-best-practices}

Adobe Engineering and Consulting teams have developed a [comprehensive set of best practices for AEM developers.](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/best-practices.html)
