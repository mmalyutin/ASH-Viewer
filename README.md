# ASH Viewer

ASH Viewer provides graphical view of active session history data within the database.

Supported databases: Oracle, PostgreSQL

![ASHViewerMainPage](media/main.png)

## Table of contents

- [Quick start](#quick-start)
- [How it works](#how-it-works)
- [Build](#build)
- [Security](#security)
- [Bugs and feature requests](#bugs-and-feature-requests)
- [Downloads](#downloads)
- [Based on](#based-on)
- [License](#license)
- [Contact](#contact)

## Quick start
- [Download the latest binary file.](https://github.com/akardapolov/ASH-Viewer/releases)
- Download JDBC driver for your database ([Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html), [PostgreSQL](https://jdbc.postgresql.org/download.html))
- Unpack the binary archive and run ASH-Viewer.jar
- Open connection dialog and populate them with data (URL for Oracle database: **jdbc:oracle:thin:@host:port:SID**)

 ![ASHViewerConnectionDialog](media/connection.png)
- Press Connect button and start to monitor your system and highlight a range to show details.

 ![ASHViewerTop](media/top.png)
- Review Raw data interface to gain a deep insight into active session history

![ASHViewerRaw](media/raw.png)
- Double-click on Top sql & sessions interface to get window with ASH details by sql or session ID

   i. SQL
 ![ASHViewerSql](media/sql.png)

   ii. Session
 ![ASHViewerSession](media/session.png)

## How it works
Active Session History (ASH) is a view in Oracle database that maps a circular buffer in the SGA.
  The name of the view is V$ACTIVE_SESSION_HISTORY. This view is populated every second
  and will only contain data for 'active' sessions, which are defined as sessions
  waiting on a non-idle event or on a CPU.
  
ASH Viewer provides graphical Top Activity, similar Top Activity analysis and Drilldown
    of Oracle Enterprise Manager performance page. ASH Viewer store ASH data locally using
    embedded database Oracle Berkeley DB Java Edition.
    
For Oracle standard edition and PostgreSQL, ASH Viewer emulate ASH, storing active session data on local storage.
  
** Please note that v$active_session_history is a part of the Oracle Diagnostic Pack and requires a purchase of the ODP license.**

## Build

```shell
mvn clean package -DskipTests=true
```

## Security
Encryption and Container settings provide security for database passwords (go to Other tab -> Security block)

### Encryption
Encryption setting has AES and PBE options
- **AES** - Advanced Encryption Standard (AES) with 256-bit key encryption, from the [Bouncy Castle provider](https://www.bouncycastle.org/), [FIPS](https://www.nist.gov/standardsgov/compliance-faqs-federal-information-processing-standards-fips#:~:text=are%20FIPS%20developed%3F-,What%20are%20Federal%20Information%20Processing%20Standards%20(FIPS)%3F,by%20the%20Secretary%20of%20Commerce.) compliant algorithm;
- **PBE** - Password based encryption (PBE) in PBEWithMD5AndDES mode with secret key (computer name or hostname). This option is weak and deprecated, please use AES when possible;

### Container
It's the way to store your encrypted data
- **DBAPI** - You sensitive data stored in Windows Data Protection API (DPAPI), maximum protected, Windows only;
- **Registry** - OS System registry storage using java preferences API - weak, but better than **Configuration**;
- **Configuration** - All data in local configuration file - weak, not recommended;

### Recommendations 
- use AES encryption and Windows Data Protection API (DPAPI) whenever possible;
- do not use PBE copied configuration on another host, you need to change password with a new secret key (always do it for password leak prevention).

## Bugs and feature requests
Have a bug or a feature request? [Please open an issue](https://github.com/akardapolov/ASH-Viewer/issues)  
  
## Downloads
- [Current version](https://github.com/akardapolov/ASH-Viewer/releases)
- [Old release 3.5.1 on github.com](https://github.com/akardapolov/ASH-Viewer/releases/tag/v3.5.1)
- [Mirror on sourceforge.net](https://sourceforge.net/projects/ashv/files/)   
  
## Based on
- [JFreeChart by David Gilbert](http://www.jfree.org)
- [E-Gantt Library by Keith Long](https://github.com/akardapolov/ASH-Viewer/tree/master/egantt)
- [Berkeley DB Java Edition](http://www.oracle.com/database/berkeley-db)
- [SwingLabs GUI toolkit by alexfromsun, kleopatra, rbair and other](https://en.wikipedia.org/wiki/SwingLabs)
- [Dagger 2 by Google](https://dagger.dev/)
- [AES cipher by Bouncy Castle](https://www.bouncycastle.org/)
- [Windows DPAPI Wrapper by @peter-gergely-horvath](https://github.com/peter-gergely-horvath/windpapi4j)

## License
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

  Code released under the GNU General Public License v3.0
  
## Contact
  Created by [@akardapolov](mailto:akardapolov@gmail.com) - feel free to contact me!