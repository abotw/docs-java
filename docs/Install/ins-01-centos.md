# Java Installation: CentOS

## 1. What Is Java and Why Install It?

Java is a widely used programming language and runtime environment.
Many tools and services (Hadoop, Hive, Elasticsearch, Jenkins, etc.) **require Java** to run.

On Linux, Java usually means installing a **JDK (Java Development Kit)**, which includes:

-   JRE (Java Runtime Environment)
-   Compiler (`javac`)
-   Useful development tools

------

## 2. Check If Java Is Already Installed

Open a terminal and run:

```bash
java -version
```

### Possible results:

-   **Java is installed** → version information is shown
-   **Java is not installed** → `command not found`

If Java is missing or the version is not what you want, continue below.

------

## 3. Choose Which Java Version to Install

For beginners, **OpenJDK** is strongly recommended:

-   Free and open source
-   Officially supported on CentOS
-   Stable and widely used

Common choices:

| Java Version | Recommended For                   |
| ------------ | --------------------------------- |
| Java 8 (1.8) | Legacy systems, Hadoop ecosystem  |
| Java 11      | Long-Term Support (LTS)           |
| Java 17      | Newer LTS (if system supports it) |

👉 If you are unsure, **Java 8 or Java 11** is a safe choice.

------

## 4. Update System Package Index (Recommended)

Before installing anything:

```bash
sudo yum update -y
```

------

## 5. Install Java Using `yum` (Recommended Way)

### 5.1 List Available Java Versions

```bash
sudo yum search openjdk
```

You’ll see packages like:

-   `java-1.8.0-openjdk`
-   `java-11-openjdk`
-   `java-17-openjdk`

------

### 5.2 Install Java 8 (Example)

```bash
sudo yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
```

Explanation:

-   `openjdk` → runtime
-   `openjdk-devel` → compiler (`javac`) and development tools

------

### 5.3 Install Java 11 (Alternative)

```bash
sudo yum install -y java-11-openjdk java-11-openjdk-devel
```

------

## 6. Verify Java Installation

After installation:

```bash
java -version
```

Expected output example:

```text
openjdk version "1.8.0_392"
OpenJDK Runtime Environment
OpenJDK 64-Bit Server VM
```

Check the compiler:

```bash
javac -version
```

------

## 7. Manage Multiple Java Versions (Optional but Important)

If multiple Java versions are installed:

```bash
sudo alternatives --config java
```

You’ll see something like:

```text
There are 2 programs which provide 'java'.

1 /usr/lib/jvm/java-1.8.0-openjdk/bin/java
2 /usr/lib/jvm/java-11-openjdk/bin/java
```

Enter the number you want to use and press **Enter**.

------

## 8. Set JAVA_HOME Environment Variable (Recommended)

Many Java-based tools **require `JAVA_HOME`**.

### 8.1 Find Java Installation Path

```bash
sudo alternatives --display java
```

Typical path example:

```text
/usr/lib/jvm/java-1.8.0-openjdk
```

------

### 8.2 Set JAVA_HOME (System-Wide)

Edit `/etc/profile`:

```bash
sudo vi /etc/profile
```

Add at the end:

```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```

Apply changes:

```bash
source /etc/profile
```

Verify:

```bash
echo $JAVA_HOME
```

------

## 9. Test Java with a Simple Program (Optional)

Create a test file:

```bash
vi HelloWorld.java
```

Paste:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java on CentOS!");
    }
}
```

Compile and run:

```bash
javac HelloWorld.java
java HelloWorld
```

Output:

```text
Hello, Java on CentOS!
```

🎉 Java is working!

------

## 10. Common Problems and Solutions

### ❌ `java: command not found`

-   Java is not installed
-   Or `PATH` is not configured correctly

### ❌ Wrong Java version

Use:

```bash
sudo alternatives --config java
```

### ❌ `JAVA_HOME is not set`

Set `JAVA_HOME` as shown in section 8

------

## 11. Summary

-   Use **OpenJDK** on CentOS
-   Install via `yum` (simple and safe)
-   Verify with `java -version`
-   Set `JAVA_HOME` for compatibility
-   Java 8 / 11 are best for beginners

