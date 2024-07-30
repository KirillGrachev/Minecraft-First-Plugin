# Getting Started with Minecraft Plugin Development: Your First Plugin for Minecraft 1.16.5

Welcome, aspiring Minecraft developers! If you're eager to start creating custom plugins for your Minecraft server, you're come to the right place. In this guide, we'll walk you through the process of creating your first Minecraft plugin. Our goal will be to make a simple plugin that sends a title message to players when they join the server.

## Prerequisites
Before we begin, make sure you have the following:
1. **Java Development Kit (JDK)**: Download and install JDK 8 to JDK 16 from [Oracle's official website](https://www.oracle.com/java/technologies/javase/jdk16-archive-downloads.html).
2. **Integrated Development Environment (IDE)**: IntelliJ IDEA or Eclipse are popular choices for Java development.
3. **Minecraft Server**: Set up a Minecraft server running version 1.16.5. You can download the server software from the [official Minecraft website](https://www.minecraft.net/en-us/download/server).
4. **Build Tool**: We'll use Maven to manage our project dependencies. Ensure Maven is installed and configured on your system.

## Step 1: Setting Up Your Working space
Firstly, if there is no JDK from version 8 to 16 on your computer, we need to download it from the official website.

**1. Go to the website and see the page shown in the screenshot below**
![first](https://github.com/user-attachments/assets/a8a7ff91-7e7d-4827-8678-480a56e2f206)

**2. After we have gone down on this page, we see links to download 16 JDK. We are downloading the newest version of JDK**
![second](https://github.com/user-attachments/assets/f283aa82-7b92-4a2a-b83b-8b1306ba9388)

**3. Create a New Maven Project**

Open your IDE and create a New Maven project. Set the GroupId to `com.example` and the ArtifactId to `FirstPlugin`.

**4. Project Structure**

Ensure your project structure looks like this:

```
FirstPlugin/
├── src/
│ ├── main/
│ │ ├── java/
│ │ │ └── com/
│ │ │ └── example/
│ │ │ └── FirstPlugin.java
│ │ └── resources/
│ │ └── plugin.yml
└── pom.xml
```

## Step 2: Configuring `pom.xml`
Open the `pom.xml` file and add the following dependencies for the Spigot API:

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.example</groupId>
  <artifactId>FirstPlugin</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <name>FirstPlugin</name>

  <properties>
    <java.version>1.8</java.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>${java.version}</source>
          <target>${java.version}</target>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>3.2.4</version>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
      </resource>
    </resources>
  </build>

  <repositories>
      <repository>
          <id>spigotmc-repo</id>
          <url>https://hub.spigotmc.org/nexus/content/repositories/snapshots/</url>
      </repository>
      <repository>
          <id>sonatype</id>
          <url>https://oss.sonatype.org/content/groups/public/</url>
      </repository>
  </repositories>

  <dependencies>
      <dependency>
          <groupId>org.spigotmc</groupId>
          <artifactId>spigot-api</artifactId>
          <version>1.16.5-R0.1-SNAPSHOT</version>
          <scope>provided</scope>
      </dependency>
  </dependencies>
</project>
```

## Step 3: Writing the Plugin Code
Navigate to `src/main/java/com/example/FirstPlugin.java` and add the following code:

```
package com.example;

import org.bukkit.plugin.java.JavaPlugin;
import org.bukkit.event.Listener;
import org.bukkit.event.EventHandler;
import org.bukkit.event.player.PlayerJoinEvent;
import org.bukkit.Bukkit;
import org.bukkit.entity.Player;

public class FirstPlugin extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        Bukkit.getPluginManager().registerEvents(this, this); // Register our event listener
    }

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent event) {
        Player player = event.getPlayer();
        player.sendTitle("Welcome", player.getDisplayName(), 10, 70, 20);
    }
}
```

## Step 4: Creating the `plugin.yml` File
Navigate to `src/main/resources/plugin.yml` and add the following content:

```
name: FirstPlugin
version: 1.0
main: com.example.FirstPlugin
api-version: 1.16
```

## Step 4: Building and Running Your Plugin

**1.Build Your Plugin** 
Run `mvn clean package` in your project's root directory. This command compiles your code and creates a JAR file in the `target` directory.

**2. Deploy Your Plugin**
Copy the generated `FirstPlugin-1.0-SNAPSHOT.jar` file from the `target` directory into the `plugins` folder in your Minecraft server.

**Start Your Server**
Start your Minecraft server. If everything is set up correctly, your plugin will be loaded, and you'll see a welcome message whenever a player joins the server.

Congratulations! You've just created your first Minecraft plugin ;)
