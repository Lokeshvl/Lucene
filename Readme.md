# Apache Lucene 10.3.2 – Installation & Demo Execution (Windows)

This document describes the complete process I followed to install, configure, and successfully run the Apache Lucene demo on Windows using Java 21.

---

## 1. Environment Setup

### Operating System
- Windows 10 /  11

### Java Version
Lucene 10 requires **Java 21 or higher**.

#### Verify Java Installation
```powershell
java -version
Expected output:

```text
java version "21"
```
2. Downloading Apache Lucene
I downloaded the binary distribution (not the source).

- **Correct:** `lucene-10.3.2.tgz`
- **Not for demo:** `lucene-10.3.2-src.tgz`
The binary package contains compiled JAR files required to run the Lucene demo.

This setup is for Apache Lucene.

3. Extracting the Archive
The .tgz file was extracted and placed at:

```text
C:\Users\LOKESH\lucene-10.3.2
```
Key directory used:

```text
C:\Users\LOKESH\lucene-10.3.2\modules
```
This folder contains:

lucene-core-10.3.2.jar

lucene-demo-10.3.2.jar

lucene-analysis-common-10.3.2.jar

lucene-queryparser-10.3.2.jar

4. Understanding Lucene 10 Demo Structure
Unlike older versions, Lucene 10:

Does NOT expose IndexFiles.java directly

Packages demo classes inside lucene-demo-10.3.2.jar

Demo classes used:

org.apache.lucene.demo.IndexFiles

org.apache.lucene.demo.SearchFiles

5. Preparing Documents for Indexing
I created a folder for raw text documents:

```powershell
cd C:\Users\LOKESH\lucene-10.3.2\modules
mkdir docs
```
Created a sample document:

```powershell
notepad docs\file1.txt
```
Sample content:

```text
Lucene 10 indexing demo.
Apache Lucene search works.
```
6. Indexing Documents
I ran the indexing command using the Lucene demo JARs.

```powershell
java -cp "lucene-demo-10.3.2.jar;lucene-core-10.3.2.jar;lucene-analysis-common-10.3.2.jar" ^
  org.apache.lucene.demo.IndexFiles -docs docs -index index
```
**Result (example):**

```text
Indexing to directory 'index'...
adding docs\file1.txt
Indexed 1 documents in 123 ms
```
This created a Lucene index in:

```text
C:\Users\LOKESH\lucene-10.3.2\modules\index
```
7. Searching the Index
To search, I included the queryparser module (required for parsing queries).

```powershell
java -cp "lucene-demo-10.3.2.jar;lucene-core-10.3.2.jar;lucene-analysis-common-10.3.2.jar;lucene-queryparser-10.3.2.jar" ^
  org.apache.lucene.demo.SearchFiles -index index -query lucene
```
**Result (example):**

```text
Searching for: lucene
1 total matching documents
1. docs\file1.txt
```